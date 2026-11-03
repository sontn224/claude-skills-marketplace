# INVEST và cách cắt story

## 6 tiêu chí INVEST: câu hỏi kiểm cho từng story

| Tiêu chí | Câu hỏi kiểm | Dấu hiệu không đạt | Cách sửa |
|---|---|---|---|
| Independent | Làm story này có cần xong story khác trước không? | "Sau khi US-02 xong mới làm được" | Đổi thứ tự, gộp, hoặc ghi phụ thuộc và chấp nhận ⚠ |
| Negotiable | Story nói cái gì cần, hay đã áp cách làm? | Có tên bảng, API, màu nút | Bỏ chi tiết giải pháp, để team thương lượng |
| Valuable | Người dùng hoặc doanh nghiệp nhận được gì? | "Để hệ thống có bảng X" | Viết lại phần "để...", hoặc gộp vào story có giá trị |
| Estimable | Team đoán được cỡ việc chưa? | Thiếu tài liệu hệ thống ngoài, rule mơ hồ | Ghi ⚠ kèm câu hỏi mở; cân nhắc spike |
| Small | Xong trong một sprint, lý tưởng vài ngày? | Quá nhiều AC (hơn khoảng 8) hoặc nhiều vai khác nhau | Tách theo mẫu bên dưới |
| Testable | Có AC kiểm chứng được không? | AC dùng "nhanh", "dễ dùng" | Thay bằng số đo hoặc trạng thái quan sát được |

## Quy tắc cắt story từ use case (cố định)
1. Main flow cùng exception nghiệp vụ (hết hàng, quá hạn công nợ) là một story.
2. Mỗi alternative (A1, A2...) là một story riêng.
3. Nhóm exception hạ tầng (hệ thống ngoài không phản hồi, mất mạng) là một story chung, kể cả khi chúng xảy ra ở nhiều bước.
4. Bước do vai khác thực hiện (người duyệt) là story riêng, kể cả khi spec đặt trong một alternative; nếu spec nói đó là use case khác thì truy vết sang use case đó.
5. Story có hơn khoảng 8 AC thì tách tiếp theo nhóm AC, và ghi lý do.
6. Không cắt theo tầng ("làm giao diện", "làm API"), vì story đó không đứng riêng được.

## Câu story
Là `<vai trong spec>`, tôi muốn `<hành động hoặc khả năng>`, để `<giá trị quan sát được>`.
- Phần "để" không được lặp lại phần "tôi muốn".
- Một vai, một việc. Hai vai thì tách hai story.
- Ghi truy vết (UC, BR, R) ngay dưới câu story, không nhét vào câu.
