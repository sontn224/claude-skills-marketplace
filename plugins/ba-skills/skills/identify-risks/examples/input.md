# Input mẫu: identify-risks (case Đại Việt Electric)

## Yêu cầu của người dùng
"Lập risk register cho Phase 1 của dự án cổng đại lý Đại Việt Electric. Dùng thang mẫu 5x5. Người phụ trách ghi bằng vai."

## Phạm vi và kế hoạch
- Phạm vi: Phase 1, cổng đại lý + CRM nội bộ gồm đăng ký đại lý, báo dự án, đặt hàng và theo dõi đơn, kết nối ERP, import đại lý cũ.
- Kế hoạch: dự án 5 tháng, Phase 1 là 3 tháng `[GIẢ ĐỊNH]`. Thời điểm lập register: Giám đốc Kinh doanh vừa đưa Change Request, còn 3 sprint x 2 tuần, backlog đã kín.
- Hội nghị đại lý có lịch cố định, không dời. Ngày cụ thể chưa có trong đầu vào.

## Tài liệu người dùng cung cấp
**S1 - Phạm vi và quyết định mở (trích).** Phase 1 như trên; Phase 2 (2 tháng `[GIẢ ĐỊNH]`) gồm bảo hành, báo cáo doanh số. Ngoài phạm vi: app nhà thầu, thanh toán online, sửa ERP, đa ngôn ngữ. Nền tảng cổng đại lý (web tùy biến hay Salesforce) chưa chốt. Tài liệu kỹ thuật kết nối ERP chưa có. SSO nội bộ chỉ dành cho nhân viên.

**S2 - Ràng buộc về nguồn lực và quy trình (trích).** Kế toán trưởng (chủ ERP) họp 1 buổi/tuần; sửa ERP nằm ngoài phạm vi dự án. Giám đốc Kinh doanh (sponsor) đặt mục tiêu R1 về tỷ lệ đơn qua cổng và thời gian xác nhận. Chủ đại lý Nhân Phát (Đà Nẵng) đang đặt hàng qua điện thoại ("gọi điện còn nhanh hơn"). Quản trị hệ thống yêu cầu phân quyền và bảo mật được xem xét (R7).

**S3 - Change Request.** Giám đốc Kinh doanh yêu cầu giao diện tiếng Anh (F8) và đăng nhập SSO cho đại lý (F9). Còn 3 sprint x 2 tuần, backlog kín, đa ngôn ngữ đã nằm ngoài phạm vi, hội nghị đại lý không dời.

**S4 - Nhu cầu thô và quy tắc liên quan (trích).** R1: 70% đơn đại lý qua cổng, thời gian từ nhận đơn đến xác nhận từ 2 ngày xuống 4 giờ `[GIẢ ĐỊNH]`. R5: đặt hàng trên điện thoại, vài bước. R8: import ~300 đại lý cũ từ Excel và ERP, lọc trùng, đại lý không phải đăng ký lại. R9: sales khu vực xem hết đơn và dự án mọi đại lý, cả vùng khác, mâu thuẫn với BR-D5 (đại lý chỉ xem dự án của mình) và nguyên tắc phân quyền theo vùng, chưa làm rõ. R12: mạng yếu vẫn dùng được, không sập cuối tháng. Hồ sơ đại lý hiện trùng, thiếu. Hợp đồng hiện có ~200 đại lý.

**S5 - Nhóm đại lý nòng cốt.** ~20% đại lý tạo 70% doanh số `[GIẢ ĐỊNH]`.

## Vai có thể làm người phụ trách
Từ case: Giám đốc Kinh doanh, TP Quản lý kênh, Kế toán trưởng, Quản trị hệ thống. Vai dự án chưa có trong case: PM, BA, Tech lead (gắn `[GIẢ ĐỊNH]`).

## Không có trong đầu vào
Ngày hội nghị đại lý, ngân sách, ước lượng effort, danh sách thành viên đội dự án, chất lượng thực tế của dữ liệu đại lý cũ.
