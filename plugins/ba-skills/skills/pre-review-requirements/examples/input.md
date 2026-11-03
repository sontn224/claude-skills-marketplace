# Input mẫu: pre-review-requirements

Dữ liệu hư cấu của case Đại Việt Electric. Mọi tên riêng và số liệu là giả định.

## Yêu cầu của BA
Review sơ bộ danh sách nhu cầu thô R1–R12 (bản nháp v0.1 `[GIẢ ĐỊNH: số phiên bản]`) trước buổi review với Giám đốc Kinh doanh và TP Quản lý kênh. Đối chiếu với phạm vi, business rule báo dự án và danh sách tính năng ứng viên bên dưới.

## Phạm vi dự án
- Phase 1 (3 tháng): cổng đại lý + CRM nội bộ: đăng ký đại lý, báo dự án, đặt hàng và theo dõi đơn, kết nối ERP, import đại lý cũ (~300).
- Phase 2 (2 tháng): bảo hành, báo cáo doanh số.
- Out of scope: app cho nhà thầu, thanh toán online, sửa ERP, đa ngôn ngữ.
- Công ty hiện có khoảng 200 đại lý ký hợp đồng theo năm.
- Hệ thống ngoài: ERP (giá niêm yết, tồn kho, đơn hàng, công nợ) · Email · SSO nội bộ (chỉ nhân viên).
- Tài liệu kỹ thuật kết nối ERP: chưa có.

## Tài liệu tham chiếu
Business rules báo dự án:
- BR-D1 Trùng khi giống cả ba: tên dự án, chủ đầu tư, tỉnh/thành.
- BR-D2 Mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ.
- BR-D3 Bảo hộ 90 ngày kể từ ngày duyệt `[GIẢ ĐỊNH]`.
- BR-D4 Báo sau, trùng dự án đang bảo hộ thì thông báo bị trùng.
- BR-D5 Đại lý chỉ xem dự án do chính mình báo.

Business rules khác liên quan:
- BR-P1 Phân quyền theo vùng `[GIẢ ĐỊNH]`, chưa có văn bản; liên quan R9 và BR-D5.
- BR-C7 Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo. Đại lý trả chậm 30–45 ngày tùy hạng `[GIẢ ĐỊNH]`.

Tính năng ứng viên: F1 Đăng ký đại lý · F2 Báo dự án · F3 Đặt hàng · F4 Theo dõi đơn · F5 Duyệt chiết khấu · F6 Yêu cầu bảo hành · F7 Báo cáo doanh số đại lý · F8 Đa ngôn ngữ · F9 Đăng nhập SSO cho đại lý.

## Tài liệu cần review: nhu cầu thô R1–R12
| Mã | Người nêu | Nội dung |
|---|---|---|
| R1 | Giám đốc Kinh doanh (Anh Quang) | 70% đơn đại lý qua cổng; thời gian từ nhận đơn đến xác nhận từ 2 ngày xuống 4 giờ `[GIẢ ĐỊNH]`. |
| R2 | TP Quản lý kênh (Chị Hạnh) | Không gõ lại đơn vào ERP. |
| R3 | Chủ đại lý Nhân Phát (Anh Nhân) | Biết đơn đang ở đâu, bao giờ giao, không phải gọi. |
| R4 | Chị Hạnh | Báo ngay nếu dự án đã có đại lý khác báo. |
| R5 | Anh Nhân | Đặt hàng được trên điện thoại, vài bước. |
| R6 | Kế toán trưởng (Chị Loan) | Giá và tồn kho lấy từ ERP; không ai sửa giá trên cổng. |
| R7 | Quản trị hệ thống (Anh Kiên) | Mật khẩu mạnh, khóa sau 5 lần sai, lưu vết mọi thao tác duyệt (ai, lúc nào). |
| R8 | Chị Hạnh | Import ~300 đại lý cũ từ Excel và ERP, lọc trùng, đại lý không phải đăng ký lại. |
| R9 | Anh Quang | Sales khu vực xem hết đơn và dự án của mọi đại lý, cả vùng khác. |
| R10 | Anh Quang | App cho nhà thầu. |
| R11 | Chị Loan | Đại lý quá hạn công nợ thì không đặt đơn mới, hoặc kế toán được báo trước khi đơn vào ERP. |
| R12 | Chị Hạnh | Cổng mở nhanh, mạng yếu vẫn dùng được, không sập cuối tháng. |
