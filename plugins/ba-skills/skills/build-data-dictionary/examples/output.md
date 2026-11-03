# Data Dictionary: Đơn hàng (DON_HANG) và Dòng đơn (DONG_DON), cổng đại lý Đại Việt Electric

## 1. Phạm vi và quy ước
- Phạm vi: 2 thực thể DON_HANG (10 trường) và DONG_DON (5 trường) lấy từ ERD của `draft-data-model`. SAN_PHAM, PHE_DUYET_CK, DAI_LY ngoài phạm vi lần này; trường nào trỏ sang đó chỉ ghi là tham chiếu.
- Nhãn nguồn: `ERP-đọc` (ERP là nguồn sự thật, cổng chỉ đọc hoặc chụp lại, không ai sửa trên cổng theo BR-C2) · `Cổng-nhập` · `Cổng-sinh` · `Cổng-tính` · `SSO`.
- Quy ước định dạng: ngày lưu theo ISO 8601 (`YYYY-MM-DD`), hiển thị `DD/MM/YYYY`; ngày giờ kèm múi giờ UTC+7; tiền là VND, không thập phân; phần trăm viết dạng `7,50` nghĩa là 7,5%. Toàn bộ quy ước này là `[GIẢ ĐỊNH]` vì chưa có tài liệu kỹ thuật ERP.
- Dữ liệu mẫu trong đầu vào chỉ dùng để gợi ý định dạng; các ví dụ dưới đây là giá trị bịa `[GIẢ ĐỊNH]`.

## 2. Bảng trường
### 2.1 DON_HANG (Đơn hàng)
| Trường | Định nghĩa | Định dạng | Giá trị hợp lệ | Bắt buộc | Nguồn | Nhạy cảm |
|---|---|---|---|---|---|---|
| ma_don | Mã định danh duy nhất của một đơn trên cổng, hiển thị cho đại lý và nhân viên | Chuỗi `DH-` + năm 4 số + `-` + 6 số, ví dụ `DH-2026-000101` `[GIẢ ĐỊNH]` | Duy nhất; không đổi sau khi tạo | Có | Cổng-sinh | Không |
| ma_dai_ly | Đại lý đặt đơn; tham chiếu `DAI_LY.ma_dai_ly` | Chuỗi, ví dụ `DL-0007` `[GIẢ ĐỊNH]` | Phải tồn tại và đại lý ở trạng thái hoạt động (precondition UC-01) | Có | Cổng-sinh (lấy từ tài khoản đang đăng nhập) | Không |
| ma_don_erp | Mã đơn do ERP cấp sau khi đơn được ghi vào ERP; dùng đối soát giữa cổng và ERP | Chuỗi; ví dụ mẫu `ERP-884201`, định dạng thật do ERP quy định, chưa có tài liệu `[GIẢ ĐỊNH]` | Rỗng khi chưa ghi vào ERP (mọi trạng thái trừ Đã xác nhận, kể cả Chờ kế toán xử lý vì E2 xảy ra ở bước 7a, trước 7b ghi đơn `[GIẢ ĐỊNH]`); có giá trị khi Đã xác nhận; duy nhất khi có giá trị | Có điều kiện (từ khi Đã xác nhận) | ERP-đọc | Không |
| trang_thai | Vị trí hiện tại của đơn trong quy trình xử lý | Chuỗi, một giá trị trong mục 3 | Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận | Có | Cổng-sinh (đổi theo sự kiện hệ thống; Đã xác nhận khi ERP ghi thành công) | Không |
| ty_le_chiet_khau | Phần trăm chiết khấu áp cho cả đơn, tính trên giá niêm yết (BR-C3) | Số thập phân 2 chữ số sau dấu phẩy, đơn vị %, ví dụ `7,50` | Từ 0,00 đến 100,00 (trần tối đa chưa có, `[GIẢ ĐỊNH]`). Theo BR-C1: dưới 5,00 đại lý tự áp; từ 5,00 đến 10,00 cần TP Quản lý kênh duyệt; trên 10,00 cần Giám đốc Kinh doanh duyệt (ngưỡng `[GIẢ ĐỊNH]`) | Có, mặc định 0,00 (chiết khấu chuẩn mặc định 0% `[GIẢ ĐỊNH]`) | Cổng-nhập | Có: đại lý khác không được xem; lãnh đạo cần thấy |
| dia_chi_giao | Địa chỉ nơi nhận hàng của đơn | Chuỗi tự do, tối đa 255 ký tự `[GIẢ ĐỊNH]` | Không rỗng khi gửi đơn; được rỗng khi còn Nháp | Có khi gửi | Cổng-nhập | Có: có thể lộ công trình và khách của đại lý |
| ngay_giao_mong_muon | Ngày đại lý muốn nhận hàng, đại lý chọn khi tạo đơn | Ngày, lưu `YYYY-MM-DD`, hiển thị `DD/MM/YYYY` | Không trước ngày gửi đơn; khoảng cách tối thiểu chưa có `[GIẢ ĐỊNH]` | Có khi gửi | Cổng-nhập | Không |
| ngay_giao_du_kien | Ngày giao mà ERP hoặc kho dự kiến, trả lời câu "bao giờ giao" của đại lý (R3) | Ngày như trên | Rỗng đến khi ERP trả về | Không | ERP-đọc `[GIẢ ĐỊNH ERP cung cấp]` | Không |
| ngay_tao | Thời điểm đơn được tạo lần đầu (lưu Nháp đầu tiên) | Ngày giờ ISO 8601 kèm múi giờ, ví dụ `2026-11-03T09:30:00+07:00` | Không đổi; không sau thời điểm hiện tại | Có | Cổng-sinh | Không |
| ngay_gui | Thời điểm đại lý bấm gửi đơn | Như ngay_tao | Rỗng đến khi gửi lần đầu; đơn quay về Nháp do E3 vẫn giữ ngay_gui của lần gửi trước, ghi đè khi gửi lại `[GIẢ ĐỊNH]`; không trước ngay_tao | Có điều kiện (từ khi gửi lần đầu) | Cổng-sinh | Không |

### 2.2 DONG_DON (Dòng đơn)
| Trường | Định nghĩa | Định dạng | Giá trị hợp lệ | Bắt buộc | Nguồn | Nhạy cảm |
|---|---|---|---|---|---|---|
| ma_dong_don | Mã định danh một dòng sản phẩm trong đơn | Chuỗi `DD-` + 8 số, ví dụ `DD-00000201` `[GIẢ ĐỊNH]` | Duy nhất | Có | Cổng-sinh | Không |
| ma_don | Đơn chứa dòng này; tham chiếu `DON_HANG.ma_don` | Như ma_don | Phải tồn tại | Có | Cổng-sinh | Không |
| ma_san_pham | Sản phẩm được đặt; tham chiếu `SAN_PHAM.ma_san_pham`, mã dùng chung với ERP | Chuỗi; ví dụ mẫu `SP-0001`, định dạng thật do ERP quy định `[GIẢ ĐỊNH]` | Phải tồn tại trong danh mục SAN_PHAM (mã do ERP cấp, dùng chung với ERP); không lặp trong cùng đơn `[GIẢ ĐỊNH]` | Có | Cổng-nhập | Không |
| so_luong | Số lượng đặt của sản phẩm trong dòng | Số nguyên dương | Từ 1 trở lên và không vượt tồn kho ERP tại lúc thêm dòng (E1 UC-01); trần mỗi dòng chưa có | Có | Cổng-nhập | Không |
| don_gia_niem_yet | Giá niêm yết của một đơn vị sản phẩm tại lúc thêm dòng, chụp từ ERP để đơn không đổi khi giá đổi | Số, đơn vị VND, không thập phân, ví dụ `1.250.000` `[GIẢ ĐỊNH]` | Lớn hơn 0; không sửa được trên cổng (BR-C2) | Có | ERP-đọc (chụp lúc thêm dòng) | Không |

## 3. Giá trị liệt kê
| Trường | Giá trị | Ý nghĩa | Căn cứ |
|---|---|---|---|
| DON_HANG.trang_thai | Nháp | Đại lý lưu chưa gửi, hoặc đơn quay về để thử lại sau khi gửi không thành | UC-01 A2; E3, E4 (BA đề xuất `[GIẢ ĐỊNH]`) |
| DON_HANG.trang_thai | Chờ duyệt chiết khấu | Đại lý xin chiết khấu thêm, đơn chờ người duyệt; chưa ghi vào ERP | UC-01 A1; BR-C1, BR-C6 |
| DON_HANG.trang_thai | Chờ kế toán xử lý | Đại lý quá hạn công nợ, đơn giữ lại và Kế toán được thông báo | UC-01 E2 (bước 7a); BR-C7 |
| DON_HANG.trang_thai | Đã xác nhận | Đơn đã ghi vào ERP; đại lý nhận email xác nhận | UC-01 postcondition |

Chưa có trong case: các trạng thái sau xác nhận (đang giao, đã giao, hủy) mà F4 Theo dõi đơn có thể cần. Chưa đưa vào bảng, xem Câu hỏi mở.

## 4. Trường tính và quy tắc liên trường
| Mục | Công thức / quy tắc | Căn cứ |
|---|---|---|
| tong_tien_niem_yet (Cổng-tính, không lưu) | Tổng của `so_luong × don_gia_niem_yet` trên mọi DONG_DON thuộc đơn | UC-01 bước 5 |
| tong_tien_sau_chiet_khau (Cổng-tính, không lưu) | `tong_tien_niem_yet × (1 − ty_le_chiet_khau / 100)`; chiết khấu tính trên giá niêm yết, áp cả đơn | BR-C3 |
| Bậc duyệt chiết khấu | `ty_le_chiet_khau` < 5: tự áp. 5 ≤ giá trị ≤ 10: TP Quản lý kênh. > 10: Giám đốc Kinh doanh. Đúng 5 và đúng 10 thuộc bậc TP Quản lý kênh | BR-C1 (ngưỡng `[GIẢ ĐỊNH]`); quy ước đầu mút `[GIẢ ĐỊNH]` trong case, chờ trainer xác nhận |
| ma_don_erp và trang_thai | `ma_don_erp` chỉ có giá trị khi Đã xác nhận; rỗng ở Nháp (kể cả khi về Nháp do E3 khi ERP không phản hồi ở 7a hoặc 7b), Chờ duyệt chiết khấu và Chờ kế toán xử lý | BR-C6; E2 ở 7a, E3 ở 7a/7b `[GIẢ ĐỊNH]` |
| ngay_gui và trang_thai | `ngay_gui` rỗng nếu đơn chưa từng gửi; có giá trị ở mọi trạng thái sau lần gửi đầu, kể cả khi đơn về Nháp do E3 | UC-01 A2, E3 `[GIẢ ĐỊNH]` |
| Giá và tồn kho | Mọi giá trị giá và tồn kho hiển thị trên đơn đến từ ERP; không có điểm nhập tay nào | BR-C2 (R6) |

### Câu hỏi mở
1. `ty_le_chiet_khau` là tổng chiết khấu (gồm "chiết khấu chuẩn" ở UC-01 bước 5 và phần xin thêm) hay chỉ phần xin thêm? Chiết khấu chuẩn lấy từ đâu (hạng đại lý, ERP); ví dụ này tạm coi mặc định 0%? (Chị Hạnh và Chị Loan)
2. Có trần chiết khấu tối đa không (giá trị lớn nhất đại lý được xin)? Quy ước đúng 5% và đúng 10% thuộc bậc 5%–10% có được chấp nhận không? (Anh Quang)
3. Sau khi Kế toán xử lý đơn quá hạn công nợ (E2), đơn tự chạy tiếp bước 7b ghi vào ERP hay quay lại đại lý gửi lại? (Chị Loan)
4. Định dạng mã đơn ERP, mã sản phẩm, độ dài tối đa, đơn vị tiền và làm tròn do ERP quy định thế nào? (Chị Loan, cần tài liệu kỹ thuật ERP)
5. ERP có trả ngày giao dự kiến không, và cập nhật theo cách nào (đẩy hay cổng hỏi)? (Chị Loan)
6. F4 cần thêm trạng thái nào sau Đã xác nhận (đang giao, đã giao, hủy, giao một phần)? (Anh Nhân và Chị Hạnh)
7. Khoảng cách tối thiểu giữa ngày gửi và ngày giao mong muốn, độ dài địa chỉ, trần số lượng mỗi dòng: có ràng buộc nào không? (Chị Hạnh)
