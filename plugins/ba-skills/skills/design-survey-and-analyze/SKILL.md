---
name: design-survey-and-analyze
description: Thiết kế bộ câu hỏi khảo sát cho một nhóm đối tượng và gom câu trả lời mở thành các chủ đề có đếm số lượng, có trích dẫn và có liên hệ về yêu cầu. Dùng khi BA cần ý kiến từ nhiều người mà không thể phỏng vấn hết, hoặc đã có phản hồi dạng chữ cần tổng hợp, ví dụ "thiết kế khảo sát", "soạn bảng hỏi cho đại lý", "gom câu trả lời mở thành chủ đề". Không dùng khi chỉ có vài người cần đào sâu (dùng prepare-stakeholder-interview), cần chốt quyết định giữa các bên (dùng plan-requirements-workshop) hoặc cần sinh ý tưởng (dùng facilitate-brainstorming).
---

# Khảo sát và bảng hỏi (Survey or Questionnaire)

## 1. Mục đích
Survey or Questionnaire là cách hỏi cùng một bộ câu hỏi có cấu trúc cho nhiều người để thu thông tin nhanh và so sánh được giữa các nhóm. Nó hợp khi cần biết mức độ phổ biến của một vấn đề hoặc thói quen, kém khi cần hiểu lý do sâu hoặc khám phá điều chưa biết. Khảo sát tốt đến từ câu hỏi ngắn, một ý, thang đo nhất quán, và việc đọc kết quả có tính đến ai đã trả lời và ai không. Skill này gồm hai việc: thiết kế bộ câu hỏi, và gom câu trả lời mở thành chủ đề.

## 2. Đầu vào cần có
- Mục tiêu khảo sát: quyết định hay yêu cầu nào sẽ dựa vào kết quả.
- Đối tượng: nhóm người, quy mô, cách chia nhóm (ví dụ theo vùng, quy mô).
- Kênh gửi và thời gian trả lời tối đa (tùy chọn; thiếu thì đề xuất và gắn `[GIẢ ĐỊNH]`).
- Câu trả lời mở đã thu, đã ẩn danh (tùy chọn; có thì làm bước phân tích).

Thiếu mục tiêu hoặc đối tượng thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Viết mục tiêu thành 3–5 điều cần biết, mỗi điều trỏ về R*/BR-*/UC cần kiểm.
2. Xác định mẫu: ai nhận, ai nên trả lời thay đại lý, cách chia nhóm, tỉ lệ phản hồi mong muốn.
3. Chọn loại câu: một lựa chọn, nhiều lựa chọn, thang đo (cùng chiều, cùng số điểm), mở. Câu mở tối đa 2–3.
4. Viết câu hỏi (mã SQ1, SQ2, ...): một ý mỗi câu, từ ngữ của người trả lời, không dẫn dắt, có "Khác" và "Không biết" khi cần. Xem `references/survey-pitfalls.md`.
5. Xếp thứ tự: dễ trước khó sau, nhóm theo chủ đề, câu nhạy cảm ở cuối; ước lượng thời gian trả lời.
6. Lập kế hoạch phân tích: câu nào thống kê, câu nào mã hóa chủ đề, cách xử lý ô trống.
7. Nếu có câu trả lời mở (mã TL01, TL02, ...): đọc hết, đặt tên chủ đề (mã TM1, TM2, ...) từ nội dung câu trả lời (không đặt trước), gán mỗi câu trả lời vào một hoặc nhiều chủ đề, đếm.
8. Mỗi chủ đề ghi mô tả ngắn, số lượt, mã câu trả lời, một trích dẫn ngắn, và yêu cầu liên quan (R*).
9. Ghi giới hạn: cỡ mẫu, thiên lệch người trả lời; không kết luận phần trăm khi mẫu nhỏ.
10. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Khảo sát: <tên>
**Mục tiêu:** ... · **Đối tượng và mẫu:** ... · **Kênh / thời gian trả lời:** ...

### Bộ câu hỏi
| Mã | Câu hỏi | Loại | Lựa chọn / thang | Bắt buộc | Mục đích (trỏ về) |
|---|---|---|---|---|---|

### Kế hoạch phân tích
| Câu | Cách xử lý | Chia theo nhóm |
|---|---|---|

### Chủ đề từ câu trả lời mở (nếu có dữ liệu)
| Chủ đề | Mô tả | Số lượt | Mã câu trả lời | Trích dẫn | Liên hệ (R*) |
|---|---|---|---|---|---|
Câu chưa xếp được: <mã và lý do>.

### Giới hạn kết quả
- ...

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi câu hỏi chỉ hỏi một ý và trỏ về một điều cần biết trong mục tiêu?
- [ ] Không có câu dẫn dắt, câu phủ định kép, câu chứa thuật ngữ nội bộ người trả lời không dùng?
- [ ] Thang đo nhất quán và có lựa chọn "Khác" hoặc "Không biết" khi cần?
- [ ] Số câu và thời gian ước lượng nằm trong giới hạn đã nêu?
- [ ] Tổng số lượt trong bảng chủ đề khớp số câu trả lời (câu thuộc nhiều chủ đề được ghi rõ)?
- [ ] Giới hạn về cỡ mẫu và thiên lệch được nêu, không suy ra phần trăm từ mẫu quá nhỏ?

## 6. BA phải verify
- AI hay đặt tên chủ đề rộng đến mức câu nào cũng lọt; BA đọc lại vài câu trả lời gốc của mỗi chủ đề.
- Số đếm chủ đề do AI tự đếm có thể lệch; BA kiểm lại bằng bảng tính khi dùng để quyết định.
- Câu trả lời mơ hồ ("chậm", "khó dùng") dễ bị gán nhầm; giữ ở "chưa xếp được" rồi hỏi lại.
- Chủ đề dẫn tới yêu cầu mới phải được stakeholder xác nhận, không đưa thẳng vào backlog.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Câu trả lời mở có thể lộ tên, số điện thoại, tên khách: ẩn danh trước khi đưa vào; không hỏi thông tin định danh nếu không cần.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
