## Kế hoạch khai thác dữ liệu: tỷ lệ đơn qua cổng và thời gian xác nhận, tuần 2 sau go-live Phase 1

### A. Phạm vi và dữ liệu
- Nguồn: bảng gộp `orders_anon` (đơn tạo trên cổng và đơn sales admin nhập hộ từ email/Zalo) `[GIẢ ĐỊNH]`. Giai đoạn 14/12 đến 18/12/2026, trích 17:00 ngày 18/12/2026, giờ Việt Nam `[GIẢ ĐỊNH]`.
- Quy mô: 17 dòng, 6 cột (`order_id`, `dealer_code`, `channel`, `created_at`, `confirmed_at`, `status`). Đã ẩn danh: mã đơn tuần tự, mã đại lý băm một chiều, không có cột giá, công nợ, tên, liên hệ.
- Giới hạn: đây là mẫu minh họa 17 dòng, chưa đại diện cho cả tuần. Không có cột chiết khấu hay kết quả kiểm công nợ nên chưa tách được lý do đơn chậm. Chưa rõ `created_at` của đơn `EMAIL_ZALO` là giờ nhận hay giờ nhập.
- Dialect: PostgreSQL. Mục tiêu so sánh (R1): 70% đơn qua cổng; xác nhận trong 4 giờ (cả hai là `[GIẢ ĐỊNH]`).

### B. Câu hỏi phân tích
| ID | Câu hỏi | Gắn với | Chỉ số và định nghĩa | Ngưỡng đối chiếu |
|---|---|---|---|---|
| M0 | Dữ liệu đủ sạch để tính chưa? | Mọi chỉ số | Dòng lỗi: trùng khóa, xác nhận thiếu giờ, giờ xác nhận trước giờ tạo. Đếm riêng bản nháp (hợp lệ, chỉ để loại khỏi mẫu số) | Mong đợi 0 dòng lỗi; dòng lỗi phải báo và loại có ghi chú. Bản nháp không phải lỗi |
| M1 | Bao nhiêu phần trăm đơn đã gửi đi qua cổng? | R1 (70%) | Số đơn `PORTAL` / số đơn đã gửi (loại `Nháp`) | 70% `[GIẢ ĐỊNH]` |
| M2 | Thời gian từ ghi nhận đến xác nhận là bao lâu, theo kênh? | R1 (4 giờ) | Số giờ giữa `created_at` và `confirmed_at` của đơn "Đã xác nhận" hợp lệ; báo trung bình, trung vị, % đơn trong 4 giờ | 4 giờ `[GIẢ ĐỊNH]`; chưa rõ áp cho trung bình hay % đơn |
| M3 | Đơn nào đang bị giữ và đã giữ bao lâu? | R1; UC-01 A1, E2 | Số giờ từ `created_at` đến mốc trích xuất, với trạng thái "Chờ duyệt chiết khấu" và "Chờ kế toán xử lý" | So với 4 giờ |
| M4 | Đại lý nào còn dùng email/Zalo? | R1 (tỷ lệ qua cổng) | Số đơn theo kênh trên mỗi `dealer_code` | Chưa có ngưỡng; để định hướng hỗ trợ đại lý |

### C. Truy vấn SQL
```sql
-- M0. PostgreSQL. Kiểm chất lượng dữ liệu: so_nhap là dòng hợp lệ (không phải lỗi); hai cột sau là dòng lỗi.
SELECT COUNT(*)                                                           AS tong_dong,
       COUNT(DISTINCT order_id)                                           AS so_order_id_duy_nhat,
       COUNT(*) FILTER (WHERE status = 'Nháp')                            AS so_nhap,
       COUNT(*) FILTER (WHERE status = 'Đã xác nhận' AND confirmed_at IS NULL) AS xac_nhan_thieu_gio,
       COUNT(*) FILTER (WHERE confirmed_at < created_at)                  AS gio_xac_nhan_truoc_gio_tao
FROM orders_anon;
```
```sql
-- M1. PostgreSQL. Mẫu số = đơn đã gửi (loại Nháp).
SELECT COUNT(*)                                   AS don_da_gui,
       COUNT(*) FILTER (WHERE channel = 'PORTAL') AS don_qua_cong,
       ROUND(100.0 * COUNT(*) FILTER (WHERE channel = 'PORTAL') / COUNT(*), 1) AS ty_le_qua_cong_pct
FROM orders_anon
WHERE status <> 'Nháp';
```
```sql
-- M2. PostgreSQL. Chỉ tính đơn "Đã xác nhận" có confirmed_at hợp lệ (>= created_at).
WITH xac_nhan AS (
  SELECT channel,
         (EXTRACT(EPOCH FROM (confirmed_at - created_at)) / 3600.0)::numeric AS gio
  FROM orders_anon
  WHERE status = 'Đã xác nhận'
    AND confirmed_at IS NOT NULL
    AND confirmed_at >= created_at
)
SELECT COALESCE(channel, 'TỔNG')                                           AS kenh,
       COUNT(*)                                                             AS so_don,
       ROUND(AVG(gio), 2)                                                   AS gio_tb,
       ROUND((PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY gio))::numeric, 1) AS gio_trung_vi,
       COUNT(*) FILTER (WHERE gio <= 4)                                     AS so_don_trong_4h,
       ROUND(100.0 * COUNT(*) FILTER (WHERE gio <= 4) / COUNT(*), 1)        AS pct_trong_4h
FROM xac_nhan
GROUP BY ROLLUP (channel)
ORDER BY channel NULLS LAST;
```
```sql
-- M3. PostgreSQL. Mốc tính = thời điểm trích xuất 2026-12-18 17:00.
SELECT status, order_id, channel,
       ROUND((EXTRACT(EPOCH FROM (TIMESTAMP '2026-12-18 17:00' - created_at)) / 3600.0)::numeric, 1) AS gio_da_giu
FROM orders_anon
WHERE status IN ('Chờ kế toán xử lý', 'Chờ duyệt chiết khấu')
ORDER BY gio_da_giu DESC;
```
```sql
-- M4. PostgreSQL. Cơ cấu kênh theo đại lý (loại Nháp).
SELECT dealer_code,
       COUNT(*) FILTER (WHERE channel = 'PORTAL')     AS don_cong,
       COUNT(*) FILTER (WHERE channel = 'EMAIL_ZALO') AS don_email_zalo,
       COUNT(*)                                       AS tong
FROM orders_anon
WHERE status <> 'Nháp'
GROUP BY dealer_code
ORDER BY don_email_zalo DESC, dealer_code;
```

### D. Kết quả mẫu từ dữ liệu input
**M0**
| tong_dong | so_order_id_duy_nhat | so_nhap (hợp lệ) | xac_nhan_thieu_gio (lỗi) | gio_xac_nhan_truoc_gio_tao (lỗi) |
|---|---|---|---|---|
| 17 | 17 | 1 (DH-2026-000114) | 0 | 1 (DH-2026-000117) |

Dòng lỗi: 1 (DH-2026-000117, giờ xác nhận 09:00 trước giờ tạo 10:00 cùng ngày), loại khỏi M2. Bản nháp DH-2026-000114 là trạng thái hợp lệ nhưng chưa phải đơn đã gửi, nên chỉ loại khỏi mẫu số của M1 và M4.

**M1**
| don_da_gui | don_qua_cong | ty_le_qua_cong_pct |
|---|---|---|
| 16 | 9 | 56.3 |

**M2** (12 đơn hợp lệ: 7 cổng, 5 email/Zalo; tổng 118 giờ)
| kenh | so_don | gio_tb | gio_trung_vi | so_don_trong_4h | pct_trong_4h |
|---|---|---|---|---|---|
| EMAIL_ZALO | 5 | 18.80 | 20.0 | 0 | 0.0 |
| PORTAL | 7 | 3.43 | 2.5 | 5 | 71.4 |
| TỔNG | 12 | 9.83 | 6.0 | 5 | 41.7 |

**M3**
| status | order_id | channel | gio_da_giu |
|---|---|---|---|
| Chờ kế toán xử lý | DH-2026-000105 | PORTAL | 78.7 |
| Chờ duyệt chiết khấu | DH-2026-000109 | PORTAL | 56.0 |
| Chờ kế toán xử lý | DH-2026-000113 | EMAIL_ZALO | 31.7 |

**M4**
| dealer_code | don_cong | don_email_zalo | tong |
|---|---|---|---|
| DL-2e5d | 0 | 2 | 2 |
| DL-a07f | 0 | 2 | 2 |
| DL-e612 | 0 | 2 | 2 |
| DL-91bc | 1 | 1 | 2 |
| DL-58a1 | 2 | 0 | 2 |
| DL-7f3a | 2 | 0 | 2 |
| DL-b3d9 | 2 | 0 | 2 |
| DL-c40e | 2 | 0 | 2 |

### E. Gợi ý biểu đồ
| ID | Loại biểu đồ | Trục và đường tham chiếu | Cảnh báo |
|---|---|---|---|
| M1 | Cột chồng 100% (qua cổng / email-Zalo) theo ngày | X: ngày tạo; Y: % đơn; đường ngang 70% | Mẫu 16 đơn quá ít để vẽ theo ngày; vẽ khi có đủ số đơn/ngày |
| M2 | Strip plot hoặc box plot số giờ theo kênh | Y: giờ; đường ngang 4 giờ | Không chỉ vẽ cột trung bình: nhóm email/Zalo trải từ 6 đến 26 giờ |
| M3 | Cột ngang theo đơn | X: giờ đã giữ; tô màu theo trạng thái; đường 4 giờ | Chỉ 3 đơn, không suy ra xu hướng |
| M4 | Cột chồng theo đại lý | X: mã đại lý; Y: số đơn theo kênh | Mỗi nhóm chỉ 2 đơn (dưới 5): chỉ dùng nội bộ, không công bố từng đại lý |

### F. Đối chiếu số trước khi kết luận
| # | Số cần đối chiếu | Giá trị trong dữ liệu | Nguồn đối chiếu | Người sở hữu | Tiêu chí khớp | Trạng thái |
|---|---|---|---|---|---|---|
| 1 | Tổng đơn đã gửi trong 14/12 đến 18/12 | 16 (17 dòng, 1 Nháp) | Danh sách đơn trong ERP cùng khoảng ngày | Kế toán trưởng | Khớp tuyệt đối; lệch phải giải thích | Chưa đối chiếu |
| 2 | Số đơn "Đã xác nhận" | 13 (12 hợp lệ, 1 lệch giờ) | Đơn trạng thái "Đã xác nhận" trong ERP | Kế toán trưởng | Khớp tuyệt đối | Chưa đối chiếu |
| 3 | Ý nghĩa và múi giờ của `confirmed_at` | Cột `confirmed_at` | Cấu hình ghi giờ trên ERP và cổng | Quản trị hệ thống | Cùng một mốc và múi giờ | Chưa đối chiếu |
| 4 | Ý nghĩa `created_at` của đơn `EMAIL_ZALO` | 7 đơn | Hỏi sales admin: giờ nhận email/Zalo hay giờ nhập | TP Quản lý kênh | Biết rõ mốc bắt đầu | Chưa đối chiếu |
| 5 | DH-2026-000117 xác nhận trước khi tạo | 1 dòng | Bản ghi gốc của đơn trong ERP | Kế toán trưởng, Quản trị hệ thống | Giải thích được nguyên nhân lệch | Lệch chưa giải thích |
| 6 | Ba đơn đang giữ (DH-2026-000105, DH-2026-000109, DH-2026-000113) | 31.7 đến 78.7 giờ | ERP và danh sách công nợ, duyệt chiết khấu | Kế toán trưởng, TP Quản lý kênh | Cùng trạng thái, cùng thời điểm vào trạng thái | Chưa đối chiếu |

Quy tắc: cho tới khi các dòng 1 đến 5 khớp, mọi con số ở mục G chỉ được báo là "sơ bộ".

### G. Nhận định sơ bộ
- Trên mẫu 16 đơn đã gửi, 9 đơn (56.3%) đi qua cổng, thấp hơn mục tiêu 70% của R1 `[GIẢ ĐỊNH]` khoảng 13.7 điểm phần trăm.
- Thời gian xác nhận của 12 đơn hợp lệ: trung bình 9.83 giờ, trung vị 6.0 giờ; 5/12 đơn (41.7%) trong 4 giờ. Chưa kết luận đạt hay chưa đạt mục tiêu 4 giờ vì chưa chốt mục tiêu tính theo trung bình hay % đơn.
- Theo kênh: cổng trung bình 3.43 giờ (trung vị 2.5), email/Zalo 18.80 giờ (trung vị 20.0), 0/5 đơn email/Zalo trong 4 giờ. Đây là mô tả; chưa đủ cơ sở nói cổng "làm" đơn nhanh hơn vì nhóm đơn và nhóm đại lý ở hai kênh có thể khác nhau.
- Có 3 đơn đang bị giữ 31.7 đến 78.7 giờ, 2 trong số đó ở "Chờ kế toán xử lý". Muốn biết lý do, chuyển sang skill analyze-root-cause.
- 6 trong 7 đơn email/Zalo thuộc 3 đại lý (DL-2e5d, DL-a07f, DL-e612). Chưa biết các đại lý này chưa dùng cổng vì lý do gì.
- Toàn bộ nhận định trên là sơ bộ vì mục F chưa đối chiếu và mẫu nhỏ.

### Câu hỏi mở
1. Mục tiêu "4 giờ" của R1 tính theo trung bình, trung vị hay tỷ lệ đơn xác nhận trong 4 giờ? Cần Anh Quang (Giám đốc Kinh doanh) chốt.
2. `created_at` của đơn email/Zalo là giờ nhận hay giờ sales admin nhập? Cần Chị Hạnh (TP Quản lý kênh) hoặc sales admin trả lời, vì ảnh hưởng trực tiếp đến con số 18.80 giờ.
3. Có thể bổ sung cột cho biết đơn có xin chiết khấu thêm (UC-01 A1) và có vướng công nợ (E2) để tách lý do chậm của đơn qua cổng (1.5 đến 6 giờ)? Cần Anh Kiên (Quản trị hệ thống).
4. DH-2026-000117 có giờ xác nhận trước giờ tạo: do múi giờ, nhập tay hay lỗi đồng bộ? Cần Anh Kiên và Chị Loan (Kế toán trưởng).
5. Mẫu 17 dòng có đủ đại diện không, hay cần lấy toàn bộ đơn ít nhất vài tuần trước khi báo cáo cho Anh Quang? Cần BA lead quyết định.
