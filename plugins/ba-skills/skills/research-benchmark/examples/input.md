# Input mẫu: research-benchmark (case Đại Việt Electric)

## Yêu cầu của người dùng
"So sánh hai phương án nền tảng cho cổng đại lý của Đại Việt Electric: PA-A web tùy biến, PA-B Salesforce. Dùng sáu tiêu chí tôi đưa bên dưới. Chỉ ghi những gì có nguồn; chỗ nào chưa có thì ghi rõ cần xác minh, đừng tự điền giá hay tính năng."

## Mục đích quyết định
Chọn nền tảng cổng đại lý cho Phase 1. Người quyết định: Giám đốc Kinh doanh (sponsor), có ý kiến của Quản trị hệ thống.

## Đối tượng so sánh
- PA-A: Web tùy biến (đội dự án tự xây).
- PA-B: Salesforce.

## Tiêu chí do người dùng đưa
| ID | Tiêu chí | Mức quan trọng |
|---|---|---|
| C1 | Đáp ứng phạm vi Phase 1 trong 3 tháng | Cao |
| C2 | Kết nối ERP (giá, tồn kho, ghi đơn) | Cao |
| C3 | Phân quyền theo vùng và lưu vết thao tác duyệt | Cao |
| C4 | Dùng được trên điện thoại, mạng yếu | Trung bình |
| C5 | Chi phí và năng lực đội triển khai | Cao |
| C6 | Mở rộng cho Phase 2 và yêu cầu thay đổi (đa ngôn ngữ, đăng nhập SSO cho đại lý) | Trung bình |

## Tài liệu nguồn người dùng cung cấp
**S1 - Nhu cầu thô R1-R12 (trích).** R2: không gõ lại đơn vào ERP. R5: đặt hàng trên điện thoại, vài bước. R6: giá và tồn kho lấy từ ERP, không ai sửa giá trên cổng. R7: mật khẩu mạnh, khóa sau 5 lần sai, lưu vết mọi thao tác duyệt (ai, lúc nào). R9: sales khu vực xem hết đơn và dự án mọi đại lý, cả vùng khác (mâu thuẫn với BR-D5 đại lý chỉ xem dự án của mình và nguyên tắc phân quyền theo vùng, chưa làm rõ). R12: cổng mở nhanh, mạng yếu vẫn dùng được, không sập cuối tháng.

**S2 - Phạm vi và ràng buộc dự án (trích).** Phase 1 3 tháng `[GIẢ ĐỊNH]`: đăng ký đại lý, báo dự án, đặt hàng và theo dõi đơn, kết nối ERP, import ~300 đại lý cũ. Phase 2 2 tháng `[GIẢ ĐỊNH]`: bảo hành, báo cáo doanh số. Ngoài phạm vi: app nhà thầu, thanh toán online, sửa ERP, đa ngôn ngữ. Tài liệu kỹ thuật kết nối ERP chưa có. SSO nội bộ chỉ dành cho nhân viên. Giai đoạn sau có thể phát sinh yêu cầu giao diện tiếng Anh (F8) và đăng nhập SSO cho đại lý (F9).

**S3 - Ghi chú của người dùng (BA), không kèm tài liệu.**
- "Web tùy biến: phân quyền theo vùng chắc phải tự lập trình."
- "Salesforce: nhớ là có phân quyền theo vai trò và theo bản ghi sẵn, chưa kiểm tra theo gói hay phiên bản."
- "Chưa nhận báo giá hay ước lượng effort từ bên nào."

**S4 - Mối quan tâm của Quản trị hệ thống (trích).** Lo phân quyền và bảo mật.

## Không có trong đầu vào
Báo giá, tài liệu sản phẩm, ước lượng effort của đội, bản demo, tham chiếu khách hàng khác.
