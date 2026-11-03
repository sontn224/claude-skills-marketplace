## Pre-review: Nhu cầu thô R1–R12, Cổng đại lý Đại Việt Electric, bản nháp v0.1
**Phạm vi:** R1–R12 · **Đối chiếu với:** phạm vi dự án, BR-D1…D5, BR-P1, BR-C7, F1–F9 · **Giới hạn:** chưa có tài liệu kỹ thuật ERP; BR-P1 (phân quyền theo vùng) là `[GIẢ ĐỊNH]` và chưa có văn bản nên chỉ đối chiếu được ở mức mô tả

### Tóm tắt
| Tiêu chí | Cao | Trung bình | Thấp | Tổng |
|---|---|---|---|---|
| Đủ | 0 | 2 | 0 | 2 |
| Rõ | 0 | 3 | 0 | 3 |
| Nhất quán | 2 | 1 | 1 | 4 |
| Kiểm chứng được | 1 | 2 | 0 | 3 |
| Truy vết được | 0 | 1 | 0 | 1 |
| **Tổng** | **3** | **9** | **1** | **13** |

### Bảng lỗi
| ID | Vị trí | Tiêu chí | Vấn đề | Mức độ | Gợi ý sửa |
|---|---|---|---|---|---|
| L-01 | R9; BR-D5; BR-P1 | Nhất quán | R9 cho sales khu vực xem hết đơn và dự án của mọi đại lý, "cả vùng khác". BR-D5 giới hạn quyền xem dự án theo người báo, và BR-P1 nêu phân quyền theo vùng. Nếu BR-D5 là nguyên tắc chung cho mọi vai thì R9 trái trực tiếp; nếu BR-D5 chỉ áp cho đại lý thì R9 vẫn trái BR-P1. Văn bản không cho biết hiểu theo cách nào. Để nguyên thì không thiết kế được phân quyền và không viết được test quyền xem. | Cao | Không chọn bên nào thay BA. Hỏi: sales khu vực xem theo vùng hay toàn quốc, chỉ đọc hay được sửa; BR-D5 áp cho những vai nào. Nên chạy analyze-business-rules cho nhóm rule quyền xem. |
| L-02 | R12 | Kiểm chứng được | "nhanh", "mạng yếu vẫn dùng được", "không sập cuối tháng" đều không có chỉ số hay điều kiện đo, nên QA không viết được tiêu chí đạt. Ba ý khác nhau đang gộp trong một mã. | Cao | Tách thành ba yêu cầu. Với mỗi yêu cầu hỏi chỉ số: thời gian tải ở điều kiện mạng nào, tải cuối tháng gồm bao nhiêu người dùng hoặc đơn đồng thời, mức sẵn sàng mong muốn. Chuyển write-nfr. Không tự điền số. |
| L-03 | R10; phạm vi dự án | Nhất quán | R10 (app cho nhà thầu) nằm trong danh sách out of scope nhưng vẫn có trong danh sách yêu cầu và do sponsor nêu. Để nguyên dễ bị hiểu là sẽ làm, hoặc bị bỏ qua mà sponsor không biết. | Cao | Không xóa R10. Hỏi Anh Quang hướng xử lý: ghi nhận ngoài phạm vi và đưa vào backlog sau, hoặc mở change request nếu muốn đưa vào dự án. Gắn trạng thái rõ ngay trong danh sách. |
| L-04 | R8 | Rõ | "lọc trùng" không nói đại lý trùng khi nào. BR-D1 định nghĩa trùng cho dự án, không áp cho hồ sơ đại lý. Chưa nói nguồn nào thắng khi Excel và ERP khác nhau, và hồ sơ nghi trùng thì tự gộp hay chờ người quyết. | Trung bình | Hỏi Chị Hạnh: đại lý trùng xét theo thuộc tính nào, nguồn nào là gốc, ca nghi trùng ai quyết. Cân nhắc ghi tiêu chí thành business rule riêng. |
| L-05 | R4; BR-D2; BR-D4 | Nhất quán | R4 muốn báo khi dự án "đã có đại lý khác báo" (kể cả chưa duyệt). BR-D4 chỉ báo trùng với dự án "đang bảo hộ", mà bảo hộ chỉ có sau khi duyệt (BR-D2) và kéo dài 90 ngày (BR-D3). Dự án đang chờ duyệt hoặc đã hết hạn bảo hộ không có bên nào phủ. | Trung bình | Hỏi Chị Hạnh: báo trùng có áp cho dự án đang chờ duyệt không, và sau 90 ngày thì sao. Chốt xong thì thống nhất lại R4 hoặc BR-D4. Nên chạy analyze-business-rules. |
| L-06 | R4, R5 | Kiểm chứng được | "báo ngay" (R4) và "vài bước" (R5) không có ngưỡng. "trên điện thoại" chưa nói là trình duyệt di động hay ứng dụng, thiết bị nào. | Trung bình | Hỏi: thời gian tối đa từ lúc gửi báo dự án đến lúc có thông báo; số bước hoặc màn hình tối đa từ lúc mở đến lúc gửi đơn; thiết bị và trình duyệt cần hỗ trợ. Chốt với Chị Hạnh và Anh Nhân, không tự điền số. |
| L-07 | R11 | Rõ | R11 nêu hai phương án loại trừ nhau ("không đặt đơn mới" hoặc "kế toán được báo trước") mà không chọn. "quá hạn" chưa định nghĩa (so với hạn trả chậm 30–45 ngày tùy hạng `[GIẢ ĐỊNH]`). BR-C7 trong phần tham chiếu nghiêng về phương án sau (đơn giữ lại, Kế toán được thông báo). | Trung bình | Hỏi Chị Loan chọn phương án nào và "quá hạn" tính từ mốc nào. Sau đó thống nhất lại R11 với BR-C7. Không tự chọn phương án. |
| L-08 | R7 | Kiểm chứng được | "mật khẩu mạnh" chưa có tiêu chí. "khóa sau 5 lần sai" chưa nói khóa bao lâu và ai mở khóa. R7 gộp ba yêu cầu (mật khẩu, khóa tài khoản, lưu vết duyệt) trong một mã nên khó nghiệm thu từng phần. | Trung bình | Hỏi Anh Kiên chính sách mật khẩu cụ thể hoặc chuẩn nội bộ để tham chiếu, thời gian khóa và quy trình mở khóa. Cân nhắc tách R7 thành ba mã. |
| L-09 | R3 | Đủ | R3 cần biết "đơn đang ở đâu, bao giờ giao" nhưng chưa có danh sách trạng thái đơn đại lý cần thấy. Phần hệ thống ngoài trong input nói ERP cung cấp giá niêm yết, tồn kho, đơn hàng, công nợ; ngày giao không được nhắc nên nguồn của "bao giờ giao" chưa rõ. Chưa nói có thông báo chủ động khi trạng thái đổi không. | Trung bình | Hỏi: các trạng thái đơn đại lý cần thấy; ngày giao dự kiến lấy từ ERP hay nhập tay; có cần thông báo chủ động không. Hỏi Anh Nhân, Chị Hạnh, Chị Loan. |
| L-10 | Thiếu (liên quan R2, R6) | Đủ | Không yêu cầu nào nói điều gì xảy ra khi ERP không phản hồi hoặc trả lỗi, trong khi R2 và R6 phụ thuộc hoàn toàn vào ERP và tài liệu kỹ thuật kết nối ERP chưa có. | Trung bình | Hỏi Chị Loan và Anh Kiên hành vi mong muốn khi ERP lỗi (giữ đơn, thử lại, báo cho ai). Cân nhắc bổ sung yêu cầu mới. Xin tài liệu kỹ thuật ERP sớm. |
| L-11 | R1 | Rõ | R1 gộp hai chỉ tiêu (tỷ lệ đơn qua cổng; thời gian từ nhận đơn đến xác nhận), thiên về mục tiêu kinh doanh hơn yêu cầu hệ thống. Chưa nói thời gian đo có gồm chờ duyệt chiết khấu và chờ kế toán xử lý công nợ không. Số 70%, 2 ngày, 4 giờ đang là `[GIẢ ĐỊNH]`. | Trung bình | Hỏi Anh Quang: tách thành hai chỉ tiêu, mốc bắt đầu và kết thúc đo, có tính thời gian chờ duyệt không, số liệu nền lấy từ đâu. Cân nhắc phân loại R1 là mục tiêu/KPI. |
| L-12 | Toàn bộ R1–R12; F1–F9 | Truy vết được | Không có bảng liên kết yêu cầu với tính năng, use case, rule. R9, R10, R11, R12 không thấy tính năng tương ứng rõ ràng trong F1–F9. Chiều ngược lại, F5, F6, F7, F8, F9 không truy được về yêu cầu nào trong R1–R12 (R7 chỉ chạm tới lưu vết duyệt). | Trung bình | Bổ sung bảng R → F / UC / BR. Với F5–F9 xác nhận nhu cầu gốc do ai nêu, hoặc yêu cầu còn thiếu trong danh sách R. |
| L-13 | R8 | Nhất quán | R8 nói import ~300 đại lý cũ, phần giới thiệu công ty trong input ghi khoảng 200 đại lý ký hợp đồng theo năm. Chênh lệch có thể do đại lý ngừng hoạt động hoặc hồ sơ trùng nhưng tài liệu không nói. | Thấp | Hỏi Chị Hạnh: 300 có gồm đại lý ngừng hoạt động không, và sau lọc trùng dự kiến còn khoảng bao nhiêu. |

### Yêu cầu chưa phát hiện lỗi
R2, R6. Lưu ý: "chưa phát hiện lỗi" không có nghĩa là đúng; hai yêu cầu này vẫn bị ảnh hưởng bởi L-10 và L-12.

### Việc ngoài phạm vi review
- Phân tích sâu nhóm rule quyền xem và báo trùng (L-01, L-05): dùng analyze-business-rules.
- Chỉ số cho R12 và chính sách mật khẩu R7 (L-02, L-08): dùng write-nfr.
- Định nghĩa "quá hạn", "bảo hộ", "đại lý trùng" (L-04, L-05, L-07): dùng build-glossary.
- Tài liệu kỹ thuật ERP chưa có, ảnh hưởng L-10 và việc ước lượng.

### Câu hỏi mở
1. Anh Quang, Chị Hạnh, Anh Kiên: sales khu vực xem đơn và dự án theo vùng hay toàn quốc, chỉ đọc hay được sửa (R9, L-01)? BR-P1 (phân quyền theo vùng) đã có văn bản chưa?
2. Chị Hạnh, Anh Kiên: R12 cần đo bằng những chỉ số nào, ở điều kiện mạng và mức tải nào?
3. Anh Quang: R10 xử lý thế nào, đưa vào backlog giai đoạn sau hay mở change request?
4. Chị Hạnh: báo trùng dự án có áp cho dự án đang chờ duyệt và dự án hết hạn bảo hộ không? Đại lý trùng xét theo thuộc tính nào khi import?
5. Chị Loan: R11 chọn phương án nào, "quá hạn" tính từ mốc nào, và khi nào có tài liệu kỹ thuật ERP?
6. Chị Hạnh: con số ~300 đại lý cũ gồm những nhóm nào, vì sao khác ~200 đại lý đang ký hợp đồng?
