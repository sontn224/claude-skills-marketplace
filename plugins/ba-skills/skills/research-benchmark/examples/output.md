## Benchmark: Nền tảng cổng đại lý Đại Việt Electric (Phase 1)
Mục đích quyết định: chọn nền tảng cho Phase 1 | Đối tượng: PA-A Web tùy biến, PA-B Salesforce | Ngày: chưa ghi trong đầu vào

### 1. Nguồn đã dùng
| ID | Tài liệu | Loại nguồn | Độ tin cậy |
|---|---|---|---|
| S1 | Nhu cầu thô R1-R12 (trích) | Yêu cầu dự án | Cao cho nội dung yêu cầu; không nói gì về năng lực của từng phương án |
| S2 | Phạm vi và ràng buộc dự án (trích) | Yêu cầu dự án | Cao; số tháng là giả định của case |
| S3 | Ghi chú của BA | Ghi chú cá nhân, không kèm tài liệu | Thấp: chỉ dùng kèm nhãn `Cần xác minh` |
| S4 | Mối quan tâm của Quản trị hệ thống | Yêu cầu dự án | Trung bình |

### 2. Tiêu chí
| ID | Tiêu chí | Nguồn tiêu chí | Mức quan trọng | Ngưỡng / yêu cầu |
|---|---|---|---|---|
| C1 | Đáp ứng phạm vi Phase 1 trong 3 tháng | Người dùng; S2 | Cao | 3 tháng (S2, `[GIẢ ĐỊNH]`) |
| C2 | Kết nối ERP | Người dùng; S1 (R2, R6) | Cao | Không nhập tay lại; giá và tồn kho từ ERP |
| C3 | Phân quyền theo vùng và lưu vết duyệt | Người dùng; S1 (R7, R9), S4 | Cao | Lưu ai, lúc nào; quy tắc xem theo vùng chưa chốt (R9 mâu thuẫn BR-D5) |
| C4 | Điện thoại, mạng yếu | Người dùng; S1 (R5, R12) | Trung bình | Đặt hàng vài bước; mạng yếu vẫn dùng được |
| C5 | Chi phí và năng lực đội | Người dùng | Cao | Chưa có ngưỡng ngân sách trong đầu vào |
| C6 | Mở rộng Phase 2 và thay đổi yêu cầu | Người dùng; S2 | Trung bình | Phase 2 (bảo hành, báo cáo); F8, F9 có thể phát sinh |

### 3. Bảng so sánh
| Tiêu chí | PA-A Web tùy biến | PA-B Salesforce |
|---|---|---|
| C1 Phạm vi Phase 1 trong 3 tháng | Cần xác minh: chưa có ước lượng effort từ đội xây | Cần xác minh: chưa có ước lượng effort từ đội triển khai |
| C2 Kết nối ERP | `[GIẢ ĐỊNH]`: kết nối do đội dự án tự lập trình (suy từ định nghĩa "tùy biến"). Chưa ước lượng được vì chưa có tài liệu kết nối ERP (S2) | Cần xác minh: cách kết nối ERP của nền tảng này chưa có nguồn. Việc thiếu tài liệu ERP (S2) ảnh hưởng cả hai phương án |
| C3 Phân quyền theo vùng, lưu vết | Phân quyền theo vùng phải tự lập trình (S3). Cần xác minh | Có phân quyền theo vai trò và bản ghi sẵn (S3). Cần xác minh theo gói và phiên bản |
| C4 Điện thoại, mạng yếu | Cần xác minh: chưa có nguồn | Cần xác minh: chưa có nguồn |
| C5 Chi phí và năng lực đội | Cần xác minh: chưa có báo giá hay ước lượng effort (S3) | Cần xác minh: chưa có báo giá hay mô hình tính phí; số lượng người dùng (đại lý và nhân viên nội bộ) là đầu vào cho báo giá nhưng chưa có trong nguồn |
| C6 Mở rộng Phase 2, F8, F9 | Cần xác minh: chưa có nguồn | Cần xác minh: chưa có nguồn. Lưu ý SSO nội bộ chỉ dành cho nhân viên (S2), F9 là đăng nhập cho đại lý |

### 4. Nhận xét
- Khác biệt đã có nguồn: chưa có khác biệt nào được kiểm chứng bằng tài liệu. Hai ghi chú ở C3 (S3) chỉ là lời BA, độ tin cậy thấp.
- Ràng buộc chung cho cả hai phương án, có nguồn: tài liệu kết nối ERP chưa có (S2); quy tắc xem dữ liệu theo vùng chưa chốt vì R9 mâu thuẫn BR-D5 (S1); danh sách ngoài phạm vi gồm đa ngôn ngữ nhưng F8, F9 có thể phát sinh (S2).
- Chưa đủ cơ sở: không thể xếp hạng hay chấm điểm hai phương án theo sáu tiêu chí.

### 5. Mức sẵn sàng ra quyết định và việc cần xác minh
Kết luận: **Chưa đủ cơ sở để khuyến nghị phương án.**
| Ô (tiêu chí x đối tượng) | Cần gì | Từ ai / nguồn nào |
|---|---|---|
| C1 A, B | Ước lượng effort cho F1-F4, kết nối ERP, import trong 3 tháng | Đội xây (A); đối tác triển khai (B) |
| C2 A, B | Tài liệu kỹ thuật kết nối ERP; phương án kết nối khả thi của từng nền tảng | Kế toán trưởng (chủ ERP); đội xây; nhà cung cấp |
| C3 A, B | Tài liệu bảo mật, cách phân quyền theo vùng, lưu vết thao tác; xác nhận của Quản trị hệ thống | Tài liệu chính thức; Quản trị hệ thống |
| C4 A, B | Bản demo thử trên điện thoại, mạng yếu | Đội xây; nhà cung cấp |
| C5 A, B | Báo giá và mô hình tính phí; năng lực và chi phí đội thực tế | Nhà cung cấp; quản lý dự án |
| C6 A, B | Khả năng mở rộng cho bảo hành, báo cáo doanh số; đa ngôn ngữ và đăng nhập đại lý | Tài liệu sản phẩm; nhà cung cấp |

### Câu hỏi mở
1. Ngưỡng ngân sách và mức ưu tiên giữa chi phí và tốc độ là gì? (Giám đốc Kinh doanh)
2. Ai có thể cung cấp tài liệu kết nối ERP, và khi nào? Việc thiếu tài liệu này chặn đánh giá C2 của cả hai phương án. (Kế toán trưởng)
3. Quy tắc phân quyền theo vùng cuối cùng là gì (R9 so với BR-D5)? Câu trả lời quyết định C3. (Giám đốc Kinh doanh, Quản trị hệ thống)
4. Các ghi chú ở S3 do ai kiểm chứng và bằng tài liệu nào? (BA)
5. Tiêu chí C4, C5, C6 đã đủ chưa, hay cần thêm tiêu chí vận hành và hỗ trợ sau go-live? (Giám đốc Kinh doanh)
