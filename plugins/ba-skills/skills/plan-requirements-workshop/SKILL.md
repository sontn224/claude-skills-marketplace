---
name: plan-requirements-workshop
description: Lập kế hoạch một requirements workshop gồm agenda theo phút, vai trò từng người dự và mẫu ghi quyết định, từ mục tiêu workshop và danh sách người dự. Dùng khi BA cần đưa nhiều bên vào một phòng để làm rõ mâu thuẫn hoặc chốt rule, ví dụ "lên kế hoạch workshop yêu cầu", "soạn agenda workshop", "mẫu ghi quyết định cuộc họp". Không dùng khi chỉ cần hỏi một người (dùng prepare-stakeholder-interview), chỉ cần sinh và chấm điểm ý tưởng của team (dùng facilitate-brainstorming) hoặc cần số liệu từ đông người (dùng design-survey-and-analyze).
---

# Workshop yêu cầu (Workshops)

## 1. Mục đích
Workshops là buổi làm việc có cấu trúc của một nhóm được chọn, nhằm cùng tạo ra một sản phẩm cụ thể (danh sách yêu cầu, rule đã chốt, quyết định về phạm vi). Điểm mạnh là giải quyết mâu thuẫn ngay trước mặt các bên và đạt đồng thuận nhanh hơn trao đổi qua lại. Buổi workshop chỉ thành công khi có mục tiêu đo được, đúng người dự, người điều phối không đứng về phía nào, và quyết định được ghi lại cùng người quyết. Skill này chuẩn bị kế hoạch và mẫu ghi chép, không điều phối thay BA.

## 2. Đầu vào cần có
- Mục tiêu workshop: cần chốt hoặc tạo ra cái gì (kết quả kiểm tra được).
- Danh sách người dự: tên, vai, thái độ hoặc mối quan tâm đã biết.
- Thời lượng và hình thức (trực tiếp/online) (tùy chọn; thiếu thì đề xuất và gắn `[GIẢ ĐỊNH]`).
- Các điểm cần quyết hoặc mâu thuẫn đã biết (R*, BR-*) (tùy chọn, nên có).
- Phạm vi dự án và các hạn chế cứng (tùy chọn).

Thiếu mục tiêu hoặc danh sách người dự thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Viết lại mục tiêu thành kết quả kiểm tra được ("cuối buổi có ... đã chốt").
2. Liệt kê các điểm cần quyết, sắp theo mức phụ thuộc: điểm nào chặn điểm nào.
3. Chọn người dự cho từng điểm; ai không liên quan thì cho dự một phần hoặc báo kết quả sau.
4. Gán vai trong workshop: facilitator, scribe/timekeeper, decision owner cho từng điểm, SME, đại diện nhóm người dùng.
5. Dựng agenda theo phút: mở, hiện trạng, từng điểm cần quyết, ngoại lệ, chốt việc. Chừa đệm 10–15% thời gian.
6. Đặt luật chơi: parking lot cho ý ngoài phạm vi, cách xử lý khi không đồng thuận (escalate cho decision owner), quy tắc phát biểu.
7. Soạn danh sách chuẩn bị trước (pre-read, dữ liệu cần mang).
8. Soạn mẫu ghi quyết định có sẵn các dòng cho điểm cần quyết.
9. Nêu rủi ro workshop theo tình huống (không theo tính cách) và cách giảm; nhận xét về từng người đặt riêng ở "Phụ lục chỉ BA".
10. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Workshop: <tên>
**Mục tiêu:** ... · **Kết quả mong đợi:** ... · **Thời lượng / hình thức:** ...

### Người dự và vai trò
| Tên | Vai trong dự án | Vai trong workshop | Dự phần nào | Lưu ý |
|---|---|---|---|---|

### Agenda
| Thời gian | Nội dung | Kỹ thuật | Phụ trách | Đầu ra |
|---|---|---|---|---|

### Luật chơi và parking lot
- ...

### Chuẩn bị trước
| Ai | Việc | Hạn |
|---|---|---|

### Mẫu ghi quyết định
| Mã | Vấn đề | Phương án | Quyết định | Người quyết | Căn cứ | Việc theo sau (ai, hạn) | Trạng thái |
|---|---|---|---|---|---|---|---|

### Rủi ro workshop
| Rủi ro | Cách giảm |
|---|---|

### Phụ lục chỉ BA (không gửi chung)
- <ghi chú về người dự, nếu cần>

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```
Chi tiết kỹ thuật điều phối: `references/facilitation-tips.md`.

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mục tiêu viết thành kết quả kiểm tra được, không phải "thảo luận về ..."?
- [ ] Mỗi điểm cần quyết có đúng một decision owner và người đó có mặt?
- [ ] Tổng thời gian agenda khớp thời lượng và có đệm?
- [ ] Người nào dự một phần có lý do rõ (ví dụ nhạy cảm, không liên quan)?
- [ ] Mẫu ghi quyết định có dòng sẵn cho từng điểm và cột "người quyết", "căn cứ"?
- [ ] Có kế hoạch cho ý ngoài phạm vi và cho tình huống không đồng thuận?

## 6. BA phải verify
- AI hay xếp quá nhiều nội dung vào ít thời gian; BA tự rà số phút thực tế.
- Vai decision owner phải do tổ chức quyết; AI chỉ gợi ý theo vai chức danh.
- AI hay đưa nhận xét tính cách vào bảng người dự và rủi ro; cột "Lưu ý" chỉ nên chứa ràng buộc quy trình, còn lại để ở phụ lục chỉ BA.
- Quyết định "đã chốt" chỉ có giá trị khi người quyết xác nhận bằng văn bản sau buổi.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Nhận xét về tính cách hoặc quan hệ giữa người dự chỉ nằm ở "Phụ lục chỉ BA"; xóa phần phụ lục trước khi gửi chung.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
