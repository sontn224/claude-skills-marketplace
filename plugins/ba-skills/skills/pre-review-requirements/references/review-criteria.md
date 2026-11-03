# Tham chiếu: 5 tiêu chí và mức độ lỗi (pre-review-requirements)

## Năm tiêu chí

### 1. Đủ
Câu hỏi: yêu cầu có đủ thông tin để thiết kế và kiểm thử không? Có tình huống nào (lỗi, biên, vai khác) mà không yêu cầu nào phủ không?
Dấu hiệu lỗi: thiếu actor, thiếu điều kiện kích hoạt, thiếu nguồn dữ liệu, thiếu xử lý khi hệ thống ngoài lỗi, thiếu yêu cầu cho một tính năng đã được nêu.

### 2. Rõ
Câu hỏi: hai người đọc độc lập có hiểu giống nhau không? Một yêu cầu có đang gói nhiều ý không?
Dấu hiệu lỗi: từ chưa định nghĩa, "hoặc" giữa hai phương án chưa chọn, một mã yêu cầu chứa nhiều yêu cầu, chủ ngữ ẩn (ai làm?), lẫn mục tiêu kinh doanh với yêu cầu.

### 3. Nhất quán
Câu hỏi: yêu cầu có mâu thuẫn với yêu cầu khác, với phạm vi, với business rule, với thuật ngữ đã chốt không?
Dấu hiệu lỗi: hai yêu cầu cùng đối tượng nhưng khác kết luận; yêu cầu nằm trong danh sách out of scope; số liệu khác nhau giữa các phần của tài liệu. Mỗi lỗi nêu **hai vế** và dẫn mã cả hai. Mâu thuẫn giữa các rule thì đề nghị chạy analyze-business-rules để phân tích sâu.

### 4. Kiểm chứng được
Câu hỏi: người kiểm thử có viết được tiêu chí đạt/không đạt không? Có con số, ngưỡng và điều kiện đo (đo ở đâu, trong hoàn cảnh nào) không?
Từ mơ hồ tiếng Việt cần soi: nhanh, ngay, dễ, đơn giản, thân thiện, vài, nhiều, ít, mạnh, ổn định, mượt, linh hoạt, tối ưu, hỗ trợ tốt, thường xuyên, kịp thời, v.v., và các cụm "không bị sập", "dùng được".
Yêu cầu phi chức năng thiếu chỉ số thì gợi ý chuyển write-nfr.

### 5. Truy vết được
Câu hỏi: yêu cầu có nguồn (ai nêu, tài liệu nào) không? Có đi tới được tính năng, use case, rule, test không? Chiều ngược lại, mỗi tính năng có yêu cầu nguồn không?
Dấu hiệu lỗi: thiếu mã, thiếu người nêu, không có bảng liên kết, tính năng không truy ngược được về yêu cầu nào, yêu cầu không gắn được vào tính năng nào.
Nếu đầu vào không có danh sách tính năng thì chỉ kiểm "có nguồn không" và ghi giới hạn này ở đầu đầu ra.

## Mức độ lỗi
- **Cao:** nếu để nguyên thì thiết kế hoặc kiểm thử đi sai hướng, yêu cầu không nghiệm thu được, hoặc gây tranh chấp phạm vi. Cần quyết định trước buổi review chính thức.
- **Trung bình:** hiểu sai một phần hoặc phải hỏi lại để chốt chi tiết. Không chặn toàn bộ công việc.
- **Thấp:** trình bày, câu chữ, sai lệch nhỏ khó gây hậu quả.

## Cách ghi vị trí
- Ưu tiên mã yêu cầu (R9, US-xx). Không có mã thì dùng "mục x.y, dòng n".
- Lỗi nhất quán ghi hai vị trí, ví dụ "R9; BR-D5".
- Lỗi do thiếu (không có yêu cầu nào) ghi "Thiếu" kèm mã yêu cầu liên quan nhất.
- Lỗi toàn cục ghi "Toàn bộ" kèm phạm vi mã.

## Quy tắc gộp lỗi
- Cùng một gốc (ví dụ "chưa có tài liệu ERP" ảnh hưởng nhiều yêu cầu) thì một dòng, vị trí liệt kê các mã.
- Một yêu cầu bị nhiều tiêu chí khác nhau thì tách dòng theo tiêu chí, vì gợi ý sửa khác nhau.
- Gợi ý sửa gồm: (a) câu hỏi cần ai trả lời, (b) hướng làm rõ. Nếu cần đưa con số làm ví dụ thì gắn `[GIẢ ĐỊNH]`.
