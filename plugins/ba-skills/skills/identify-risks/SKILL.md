---
name: identify-risks
description: Lập risk register từ phạm vi và kế hoạch dự án, mỗi rủi ro có khả năng x tác động, cách ứng phó, trigger và người phụ trách. Dùng khi bắt đầu hoặc cập nhật kế hoạch, hoặc khi có thay đổi lớn về phạm vi, ví dụ "lập risk register", "nhận diện rủi ro dự án", "đánh giá rủi ro Phase 1". Không dùng khi sự việc đã xảy ra và cần hỏi vì sao (dùng analyze-root-cause), cần phân tích điểm mạnh/yếu tổng quan (dùng draft-swot), so sánh phương án theo tiêu chí (dùng research-benchmark) hoặc rút bài học sau sprint/dự án (dùng summarize-lessons-learned).
---

# Phân tích và quản lý rủi ro (Risk Analysis and Management)

## 1. Mục đích
Risk Analysis and Management là việc nhận diện những sự kiện chưa xảy ra nhưng có thể làm lệch mục tiêu, đánh giá mức độ (khả năng xảy ra và tác động), chọn cách ứng phó rồi theo dõi. Kết quả là risk register để nhóm ưu tiên nguồn lực vào chỗ nguy hiểm nhất. Rủi ro là điều **có thể** xảy ra; điều đã xảy ra là issue và xử lý qua quản lý vấn đề hoặc change control, không đưa vào bảng chấm điểm.

## 2. Đầu vào cần có
- Phạm vi và mục tiêu của kế hoạch cần đánh giá rủi ro (bắt buộc).
- Kế hoạch: các phase, mốc, ràng buộc cố định, phụ thuộc vào hệ thống hoặc người khác (bắt buộc).
- Những điều chưa quyết, chưa có, hoặc đang là giả định (bắt buộc; thiếu thì hỏi, vì đây là nguồn rủi ro chính).
- Thang chấm của tổ chức (tùy chọn). Không có thì dùng thang mẫu 5x5 trong `references/thang-cham-rui-ro.md` và ghi rõ đó là thang mẫu.
- Danh sách vai có thể làm người phụ trách (tùy chọn). Không có thì đề xuất vai và gắn `[GIẢ ĐỊNH]`.

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Chốt phạm vi, mốc thời gian, thang chấm sẽ dùng.
2. Lập bảng nguồn (S1, S2...) và đọc từng nguồn tìm: ràng buộc cứng, phụ thuộc, điều chưa quyết, giả định, nguồn lực hạn chế, yêu cầu mâu thuẫn.
   Quy tắc nền (để kết quả ổn định giữa các lần chạy): nếu nguồn có (a) tài liệu hoặc kết nối với hệ thống ngoài chưa có, (b) quyết định lớn còn mở (nền tảng, công nghệ), (c) yêu cầu thay đổi hoặc phạm vi mới chưa được quyết, (d) mốc cố định không dời, (e) nguồn lực hạn chế về lịch hoặc người, (f) dữ liệu cũ cần chuyển, (g) yêu cầu mâu thuẫn chưa giải, thì mỗi nhóm phải có ít nhất một rủi ro, hoặc ghi lý do không đưa vào.
3. Mỗi rủi ro viết dạng "Nếu <sự kiện> thì <hậu quả>", kèm nguồn. Tách rủi ro khỏi issue đã xảy ra. Cơ hội (tác động tích cực) ghi riêng loại Opportunity.
4. Chấm Khả năng (P) và Tác động (I) theo thang, nêu căn cứ. Điểm = P x I. Điểm do AI đề xuất, gắn `[GIẢ ĐỊNH]` đến khi BA/PM xác nhận.
5. Chọn chiến lược: Avoid, Mitigate, Transfer, Accept (với cơ hội: Exploit hoặc Enhance). Viết hành động cụ thể; rủi ro mức Cao trở lên có thêm kế hoạch dự phòng.
6. Mỗi rủi ro có trigger (dấu hiệu đo được cho biết rủi ro sắp xảy ra) và người phụ trách (vai) duy nhất; vai chưa có trong nguồn gắn `[GIẢ ĐỊNH]`.
7. Tổng hợp theo mức, nêu top rủi ro, các chỗ chấm điểm còn thiếu căn cứ.
8. Nêu câu hỏi mở.

## 4. Mẫu đầu ra
```
## Risk register: <phạm vi>
Kế hoạch tham chiếu: <...> | Thang chấm: <mẫu / của tổ chức> | Ngày: <...>

### 1. Nguồn đã dùng
| ID | Tài liệu | Loại nguồn |

### 2. Đánh giá rủi ro
| ID | Loại | Mô tả (Nếu... thì...) | Nguồn | P | I | Điểm | Mức (thang 5x5) | Căn cứ chấm |

### 3. Ứng phó và theo dõi
| ID | Chiến lược | Hành động ứng phó | Kế hoạch dự phòng | Trigger | Người phụ trách (vai) | Nhịp review |

### 4. Tổng hợp
| Mức | Số rủi ro | ID |
Top rủi ro cần xử lý trước: <...>

### 5. Điểm chấm thiếu căn cứ
- <rủi ro nào, P hay I, thiếu gì>

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
```
ID rủi ro dùng RK-01, RK-02... "Rất cao" chỉ là tên một mức của thang 5x5 (cột Mức và bảng Tổng hợp); mọi chỗ khác (mức quan trọng, độ tin cậy, nhận xét) dùng Cao / Trung bình / Thấp. Ví dụ đầy đủ: `examples/output.md`.

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi rủi ro có đủ nguồn, P, I, điểm tính đúng (P x I), mức khớp thang, và căn cứ chấm?
- [ ] Mỗi rủi ro có đúng một người phụ trách (vai) và một trigger đo được, không chung chung kiểu "khi có vấn đề"?
- [ ] Hành động ứng phó cụ thể làm được (ai làm gì), không chỉ "theo dõi"; rủi ro mức Cao trở lên có kế hoạch dự phòng?
- [ ] Không lẫn issue đã xảy ra vào bảng điểm; mỗi mô tả là sự kiện chưa xảy ra, dạng "Nếu... thì..."?
- [ ] Không có số ngày, số tiền, mốc nào không có trong nguồn; điểm AI đề xuất và vai chưa có trong nguồn đã gắn `[GIẢ ĐỊNH]`?
- [ ] Đầu ra kết thúc bằng "Câu hỏi mở", câu hỏi xuất phát từ chỗ thiếu thật của nguồn?

## 6. BA phải verify
- Điểm P và I do AI chấm chỉ là đề xuất. Người biết dự án (BA, PM, sponsor) phải chấm lại, nhất là tác động lên mốc cố định.
- Rủi ro AI thêm từ kinh nghiệm chung nhưng không có dấu vết trong nguồn: yêu cầu nguồn hoặc xóa.
- Người phụ trách: AI chỉ đề xuất vai; phải được người đó đồng ý, và người đó phải có quyền xử lý.
- Trigger phải đo được thực tế (ai đo, đo ở đâu); AI hay viết trigger mà không ai theo dõi được.
- Phân biệt rủi ro với issue và với yêu cầu chưa chốt; yêu cầu mâu thuẫn nên xử lý ở bước làm rõ yêu cầu, rủi ro chỉ ghi hậu quả nếu không xử lý.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Người phụ trách ghi bằng vai, không dùng tên thật khi register có thể lưu hành rộng.
- Không ghi nhận xét về tính cách hay năng lực cá nhân vào risk register; mô tả bằng ràng buộc quy trình ("chỉ họp 1 buổi/tuần"). Rủi ro về an ninh hệ thống chi tiết (lỗ hổng cụ thể) thuộc kênh riêng, không ghi ở đây.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
