Vẽ giúp tôi mind map phạm vi dự án cổng đại lý Đại Việt Electric từ ghi chú kickoff dưới đây. Mục đích: cho cả nhóm nhìn một trang trước khi bắt đầu phỏng vấn.

**Ghi chú kickoff (đã rút gọn, theo thứ tự ghi trong buổi họp)**
- Dự án 5 tháng, hai phase `[GIẢ ĐỊNH]`. Phase 1 (3 tháng): cổng đại lý và CRM nội bộ gồm đăng ký đại lý, báo dự án, đặt hàng và theo dõi đơn, kết nối ERP, import khoảng 300 đại lý cũ. Phase 2 (2 tháng): bảo hành, báo cáo doanh số.
- Out of scope: app cho nhà thầu (R10), thanh toán online, sửa ERP, đa ngôn ngữ.
- Đại lý đăng ký: F1. Import đại lý cũ từ Excel và ERP, lọc trùng, đại lý không phải đăng ký lại (R8).
- Báo dự án: F2. Báo ngay nếu dự án đã có đại lý khác báo (R4). Rule: BR-D1 trùng khi giống cả tên dự án, chủ đầu tư, tỉnh/thành; BR-D2 mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ; BR-D3 bảo hộ 90 ngày từ ngày duyệt `[GIẢ ĐỊNH]`; BR-D4 báo sau mà trùng dự án đang bảo hộ thì thông báo bị trùng; BR-D5 đại lý chỉ xem dự án do chính mình báo.
- Đặt hàng: F3, UC-01. Luồng chính 8 bước. Nhánh phụ: A1 xin chiết khấu thêm, A2 lưu nháp. Ngoại lệ: E1 không đủ tồn kho, E2 quá hạn công nợ. Đặt được trên điện thoại, vài bước (R5).
- Chiết khấu (F5): dưới 5% đại lý tự áp, 5%–10% TP Quản lý kênh duyệt, trên 10% Giám đốc Kinh doanh duyệt (các ngưỡng là `[GIẢ ĐỊNH]`).
- Theo dõi đơn: F4. Đại lý biết đơn đang ở đâu và bao giờ giao (R3).
- ERP: không gõ lại đơn (R2); giá và tồn kho lấy từ ERP, không ai sửa giá trên cổng (R6); đại lý quá hạn công nợ thì giữ đơn và báo kế toán (R11). Chưa có tài liệu kỹ thuật kết nối ERP.
- Phi chức năng: mật khẩu mạnh, khóa sau 5 lần sai, lưu vết mọi thao tác duyệt (R7); cổng mở nhanh, mạng yếu vẫn dùng được, không sập cuối tháng (R12).
- Cần quyết: nền tảng cổng đại lý (web tùy biến hay Salesforce). R9 của anh Quang (sales khu vực xem mọi đại lý, cả vùng khác) mâu thuẫn BR-D5. Anh Quang cũng yêu cầu giao diện tiếng Anh (F8) và đăng nhập SSO cho đại lý (F9).
