# Input mẫu: mine-usage-data (Đại Việt Electric, sau go-live Phase 1)

## Yêu cầu của BA
Phase 1 đã go-live. Anh Quang (Giám đốc Kinh doanh) hỏi: "Tuần thứ hai chạy, bao nhiêu phần trăm đơn đi qua cổng và đơn được xác nhận nhanh cỡ nào so với mục tiêu?". Hãy lập kế hoạch khai thác dữ liệu để trả lời hai câu: tỷ lệ đơn qua cổng so với mục tiêu 70%, và thời gian xác nhận so với mục tiêu 4 giờ (R1).

## Bối cảnh `[GIẢ ĐỊNH]`
- Go-live Phase 1: thứ Hai 07/12/2026. Dữ liệu là tuần thứ hai, thứ Hai 14/12 đến thứ Sáu 18/12/2026, trích lúc 17:00 ngày 18/12/2026, giờ Việt Nam (UTC+7).
- Mục tiêu theo R1: 70% đơn đại lý qua cổng; thời gian từ nhận đơn đến xác nhận từ 2 ngày xuống 4 giờ. Cả hai con số là `[GIẢ ĐỊNH]` trong case.
- Nguồn: bảng gộp `orders_anon` gồm đơn tạo trên cổng và đơn do sales admin nhập tay vào ERP từ email/Zalo `[GIẢ ĐỊNH]`. Hệ quản trị CSDL: PostgreSQL.
- Ẩn danh: `order_id` là mã tuần tự, `dealer_code` là mã băm một chiều. Đã bỏ các cột giá, số lượng, công nợ, tên và liên hệ.
- Đây là mẫu rút gọn 17 dòng để minh họa, không đại diện cho toàn bộ đơn của tuần (số đơn/ngày thực tế lớn hơn nhiều). Mọi con số trong bảng là bịa `[GIẢ ĐỊNH]`.
- Nguồn đối chiếu sẵn có: danh sách đơn trong ERP (chủ sở hữu: Kế toán trưởng).

## Ý nghĩa cột
| Cột | Ý nghĩa |
|---|---|
| order_id | Mã đơn đã ẩn danh |
| dealer_code | Mã đại lý băm một chiều |
| channel | `PORTAL` (tạo trên cổng) hoặc `EMAIL_ZALO` (sales admin nhập hộ) |
| created_at | Thời điểm đơn được ghi nhận (không rõ là giờ nhận email hay giờ nhập; xem Câu hỏi mở) |
| confirmed_at | Thời điểm đơn chuyển sang "Đã xác nhận"; trống nếu chưa xác nhận |
| status | Đã xác nhận / Chờ duyệt chiết khấu / Chờ kế toán xử lý / Nháp |

## Dữ liệu `orders_anon`
| order_id | dealer_code | channel | created_at | confirmed_at | status |
|---|---|---|---|---|---|
| DH-2026-000101 | DL-7f3a | PORTAL | 2026-12-14 08:10 | 2026-12-14 10:40 | Đã xác nhận |
| DH-2026-000102 | DL-91bc | PORTAL | 2026-12-14 09:30 | 2026-12-14 15:30 | Đã xác nhận |
| DH-2026-000103 | DL-2e5d | EMAIL_ZALO | 2026-12-14 09:45 | 2026-12-15 11:45 | Đã xác nhận |
| DH-2026-000104 | DL-7f3a | PORTAL | 2026-12-15 08:00 | 2026-12-15 09:30 | Đã xác nhận |
| DH-2026-000105 | DL-c40e | PORTAL | 2026-12-15 10:20 | | Chờ kế toán xử lý |
| DH-2026-000106 | DL-91bc | EMAIL_ZALO | 2026-12-15 13:00 | 2026-12-16 09:00 | Đã xác nhận |
| DH-2026-000107 | DL-58a1 | PORTAL | 2026-12-15 14:15 | 2026-12-15 16:45 | Đã xác nhận |
| DH-2026-000108 | DL-2e5d | EMAIL_ZALO | 2026-12-16 08:30 | 2026-12-17 08:30 | Đã xác nhận |
| DH-2026-000109 | DL-b3d9 | PORTAL | 2026-12-16 09:00 | | Chờ duyệt chiết khấu |
| DH-2026-000110 | DL-e612 | EMAIL_ZALO | 2026-12-16 10:10 | 2026-12-16 16:10 | Đã xác nhận |
| DH-2026-000111 | DL-c40e | PORTAL | 2026-12-16 11:00 | 2026-12-16 12:30 | Đã xác nhận |
| DH-2026-000112 | DL-58a1 | PORTAL | 2026-12-17 08:45 | 2026-12-17 14:45 | Đã xác nhận |
| DH-2026-000113 | DL-a07f | EMAIL_ZALO | 2026-12-17 09:20 | | Chờ kế toán xử lý |
| DH-2026-000114 | DL-7f3a | PORTAL | 2026-12-17 10:00 | | Nháp |
| DH-2026-000115 | DL-e612 | EMAIL_ZALO | 2026-12-17 15:00 | 2026-12-18 09:00 | Đã xác nhận |
| DH-2026-000116 | DL-b3d9 | PORTAL | 2026-12-18 08:15 | 2026-12-18 12:15 | Đã xác nhận |
| DH-2026-000117 | DL-a07f | EMAIL_ZALO | 2026-12-18 10:00 | 2026-12-18 09:00 | Đã xác nhận |

## Việc cần làm
Đưa ra kế hoạch khai thác: câu hỏi phân tích, SQL, kết quả mẫu tính từ bảng trên, gợi ý biểu đồ, và các bước đối chiếu số với ERP trước khi báo cáo cho Anh Quang.
