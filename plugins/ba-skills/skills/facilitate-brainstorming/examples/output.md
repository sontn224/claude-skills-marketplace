## Brainstorming: Đưa đơn hàng đại lý sang cổng
**Câu hỏi chủ đề:** Làm sao để đại lý chuyển phần lớn đơn hàng sang cổng, hướng tới 70% đơn qua cổng (R1) trong 3 tháng đầu sau ra mắt `[GIẢ ĐỊNH]`? · **Ràng buộc:** trong Phase 1; ngoài scope gồm app nhà thầu, thanh toán online, sửa ERP, đa ngôn ngữ; hội nghị đại lý không dời; chiết khấu theo ngưỡng duyệt hiện có (BR-C1); đại lý không được thấy hoạt động của đại lý khác (tinh thần BR-D5) · **Số ý:** 10 của team, 4 AI đề xuất

### Danh sách ý (đã mở rộng)
| Mã | Ý | Nguồn | Ghi chú |
|---|---|---|---|
| B1 | Cho đặt lại đơn cũ chỉ một chạm | Team | |
| B2 | Giao diện điện thoại, đặt hàng trong vài bước | Team | Liên quan R5 |
| B3 | Hiển thị trạng thái đơn và ngày giao dự kiến ngay trên cổng | Team | Liên quan R3 |
| B4 | Sales khu vực đến từng đại lý hướng dẫn trực tiếp | Team | |
| B5 | Ra mắt cổng tại hội nghị đại lý, cho đăng ký ngay tại chỗ | Team | Hội nghị không dời |
| B6 | Dừng nhận đơn qua Zalo và email sau một ngày chốt | Team | |
| B7 | Tặng thêm chiết khấu cho đơn đặt qua cổng | Team | |
| B8 | Video hướng dẫn 2 phút | Team | |
| B9 | Xếp hạng công khai các đại lý dùng cổng nhiều nhất | Team | |
| B10 | Hotline hỗ trợ đặt hộ trong tháng đầu | Team | |
| B11 | Import sẵn đại lý cũ để không phải đăng ký lại | AI đề xuất | Liên quan R8 (~300 đại lý) |
| B12 | Xin và duyệt chiết khấu ngay trên cổng, có thông báo tiến độ | AI đề xuất | Liên quan duyệt chiết khấu (F5), R7 |
| B13 | Khi nhận đơn qua Zalo hoặc email, sales admin gửi lại link cổng và hướng dẫn đặt lần sau | AI đề xuất | Chuyển hướng mềm, không cần sửa hệ thống |
| B14 | Cho tải file đơn Excel lên cổng | AI đề xuất | Đại lý hiện đặt bằng Excel; chưa nằm trong F1–F9 |

### Gom nhóm
| Nhóm | Ý (mã) | Ý nghĩa của nhóm |
|---|---|---|
| N1. Giảm công sức đặt hàng | B1, B2, B14 | Làm cho đặt trên cổng nhanh hơn đặt bằng Zalo hay Excel |
| N2. Minh bạch tiến độ | B3, B12 | Đại lý thấy đơn và việc duyệt đang ở đâu, không phải gọi hỏi |
| N3. Dẫn dắt hành vi và chính sách | B6, B7, B9, B13 | Thúc đẩy hoặc ràng buộc đại lý dùng cổng |
| N4. Hỗ trợ và ra mắt | B4, B5, B8, B10, B11 | Giúp đại lý bắt đầu dùng cổng |

### Chấm điểm đề xuất
| Mã | Tác động | Khả thi | Điểm | Phạm vi | Lý do |
|---|---|---|---|---|---|
| B1 | 4 | 4 | 16 | Trong scope (đặt hàng, UC-01) | Đại lý hay đặt lặp; chỉ dùng lại dữ liệu đơn cũ |
| B2 | 5 | 3 | 15 | Trong scope (R5) | Quyết định có dùng được ở công trình hay không; giao diện cần thiết kế kỹ |
| B3 | 5 | 4 | 20 | Trong scope (theo dõi đơn, R3) | Đáp thẳng R3, giảm việc phải gọi hỏi; trạng thái đơn đã có trong UC-01 |
| B4 | 3 | 3 | 9 | Vận hành | Hiệu quả cao nhưng tốn thời gian đi lại; ngân sách chưa rõ `[GIẢ ĐỊNH]` |
| B5 | 4 | 3 | 12 | Vận hành | Tận dụng hội nghị cố định; phụ thuộc cổng có bản chạy được trước hội nghị |
| B6 | 5 | 2 | 10 | Chính sách | Hiệu quả nhất nhưng rủi ro mất đơn; cần người có quyền quyết |
| B7 | 4 | 2 | 8 | Chính sách | Chạm quy tắc duyệt chiết khấu theo ngưỡng (BR-C1); ảnh hưởng doanh thu |
| B8 | 2 | 5 | 10 | Vận hành | Rẻ, nhưng chỉ giúp người đã muốn dùng |
| B9 | 2 | 3 | 6 | Chính sách | Lộ hoạt động đại lý này cho đại lý khác, trái tinh thần BR-D5 |
| B10 | 3 | 4 | 12 | Vận hành | Giảm rào cản giai đoạn đầu; tạm thời |
| B11 | 4 | 4 | 16 | Trong scope (R8) | Đại lý cũ vào thẳng, không rào đăng ký |
| B12 | 4 | 3 | 12 | Trong scope (F5, R7) | Nỗi đau chờ duyệt qua Zalo; cần luồng duyệt và thông báo |
| B13 | 3 | 5 | 15 | Vận hành | Chi phí gần như bằng không, dùng đúng thời điểm đại lý đặt qua kênh cũ |
| B14 | 4 | 2 | 8 | Ngoài scope hiện tại | Chưa có trong F1–F9; cần đánh giá qua thay đổi phạm vi |

### Đề xuất ưu tiên
1. B3 (20): trạng thái đơn và ngày giao trên cổng.
2. B1 (16): đặt lại đơn cũ một chạm.
3. B11 (16): import sẵn đại lý cũ.
4. B2 (15): giao diện điện thoại ít bước.
5. B13 (15): chuyển hướng mềm khi nhận đơn qua kênh cũ.

Mốc riêng (không đếm vào 5 ý trên): B5 (12), ra mắt tại hội nghị đại lý, vì điểm không cao nhưng ngày hội nghị không dời.

### Ý hoãn hoặc loại
| Mã | Quyết định | Lý do |
|---|---|---|
| B9 | Loại (đề xuất) | Công khai xếp hạng làm lộ thông tin giữa các đại lý, trái tinh thần BR-D5 |
| B7 | Hoãn | Chạm chính sách chiết khấu; cần anh Quang và chị Hạnh quyết |
| B6 | Hoãn | Chỉ cân nhắc sau khi tỉ lệ dùng cổng ổn định; cần anh Quang quyết |
| B14 | Hoãn | Ngoài danh sách tính năng; xét qua quy trình thay đổi phạm vi |
Điểm trên là đề xuất; team nên chấm lại bằng bỏ phiếu ẩn.

### Câu hỏi mở
1. Mục tiêu 70% đơn qua cổng cần đạt trong bao lâu sau ra mắt, 3 tháng có đúng không? (cần: anh Quang)
2. Hội nghị đại lý diễn ra khi nào, và cổng có bản chạy được trước ngày đó không? (cần: anh Quang, đội dự án)
3. Có cho phép dừng nhận đơn qua Zalo và email (B6) sau một thời điểm nào không? (cần: anh Quang, chị Hạnh)
4. Có ngân sách cho sales khu vực đi hướng dẫn trực tiếp (B4) và hotline (B10) không? (cần: anh Quang)
5. Có muốn đưa việc tải đơn Excel lên cổng (B14) vào change request không? (cần: anh Quang, BA)
