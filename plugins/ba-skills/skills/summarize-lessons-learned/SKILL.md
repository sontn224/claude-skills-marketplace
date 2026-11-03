---
name: summarize-lessons-learned
description: Tổng hợp ghi chú retrospective thành chủ đề, hành động có chủ và hạn, và danh sách lỗi AI lặp lại kèm đề xuất sửa skill trong repo ba-skills để nối vòng phản hồi. Dùng khi kết thúc sprint hoặc phase và BA có ghi chú retro, ví dụ "tổng kết bài học", "tổng hợp retro", "lessons learned sau sprint". Không dùng khi cần tìm nguyên nhân gốc của một sự cố cụ thể (dùng analyze-root-cause), khi cần đánh giá rủi ro cho giai đoạn tới (dùng identify-risks), hoặc khi chỉ cần biên bản họp thông thường.
---

# Tổng kết bài học (Lessons Learned – BABOK v3)

## 1. Mục đích
Lessons Learned là việc thu thập và đúc kết điều đã xảy ra trong một sprint hoặc phase để lần sau làm tốt hơn. Skill này làm ba việc: gom ghi chú retro thành chủ đề, biến chủ đề cần đổi thành hành động có vai chịu trách nhiệm và hạn, và tách riêng các lỗi do AI sinh ra mà **lặp lại** để đề xuất sửa đúng skill trong repo ba-skills. Phần thứ ba là vòng phản hồi: lỗi thấy ở dự án phải quay về sửa skill, nếu không lỗi sẽ lặp ở dự án sau. Skill không đánh giá cá nhân và không đào sâu nguyên nhân gốc (việc đó thuộc analyze-root-cause).

## 2. Đầu vào cần có
- Ghi chú retro: điều tốt, điều chưa tốt, ý tưởng, kèm giai đoạn (sprint hoặc phase).
- Với mỗi lỗi AI được nhắc: tài liệu hoặc sản phẩm bị lỗi, ai phát hiện, phát hiện ở đâu (review, test, demo), hậu quả. Ghi chú chỉ nói "AI viết sai" mà không rõ ở đâu thì hỏi lại.
- Danh sách skill hoặc công cụ AI đã dùng trong giai đoạn. Tùy chọn; thiếu thì suy từ loại tài liệu và gắn `[GIẢ ĐỊNH]`.
- Log lỗi AI các lần retro trước, để đếm "lặp lại" xuyên giai đoạn. Tùy chọn.
- Hành động từ retro trước, để kiểm đã làm chưa. Tùy chọn.

Thiếu ghi chú retro thì **hỏi lại người dùng trước khi làm**. Không tự bịa sự việc để lấp chỗ trống.

## 3. Các bước
1. Ẩn danh trước tiên: thay mọi tên người bằng vai trò (BA, Dev A, QA, TP Quản lý kênh, Giám đốc Kinh doanh). Không lặp tên trong kết quả, kể cả trong trích dẫn.
2. Tách ghi chú thành từng ý đơn, gắn nhãn Tốt, Chưa tốt hoặc Ý tưởng, giữ tham chiếu tới ghi chú gốc.
3. Gom theo chủ đề (tối đa khoảng 7, mã TM1, TM2...), mỗi chủ đề có ít nhất một bằng chứng trích ngắn. Đếm số lần nhắc theo nhãn của ghi chú: ghi chú Chưa tốt cho cột Đổi, Tốt cho cột Giữ; Ý tưởng không cộng vào số lần nhắc mà ghi riêng.
4. Phân loại ý "Chưa tốt" thành: lỗi quy trình hoặc con người, lỗi do AI sinh ra, yếu tố bên ngoài. Cách nhận diện nằm trong `references/ai-error-taxonomy.md`. Không đổ mọi thứ lên AI.
5. Với chủ đề cần đổi, tạo hành động: việc cụ thể, vai chịu trách nhiệm (không phải tên), hạn theo sprint, tiêu chí "xong khi". Hạn hoặc vai ghi chú không nêu thì gắn `[GIẢ ĐỊNH]` hoặc đưa vào câu hỏi mở.
6. Với lỗi AI: truy từ tài liệu bị lỗi về skill đã tạo ra nó (slug trong repo, bảng tra ở references). Lỗi là **lặp lại** khi có từ hai lần xuất hiện trở lên ở các tài liệu khác nhau hoặc các giai đoạn khác nhau. Một lần thì vào bảng theo dõi.
7. Với mỗi lỗi lặp lại, **đọc lại mục đích và các bước trong SKILL.md của skill đích** trước khi đề xuất. Nếu quy tắc đã có thì đề xuất làm cứng hơn (quy tắc đếm được, ví dụ sai), không đề xuất lặp lại. Ghi skill nào, mục nào (3 Các bước, 5 Tự kiểm hay 6 BA phải verify), quy tắc đã có là gì, thêm hoặc đổi câu gì; kèm cách kiểm tra lại (chạy lại `examples/input.md` của skill, có thể cố ý bỏ một dữ kiện để xem AI có bịa lại không).
8. Chỉ đề xuất, không tự sửa skill. Xếp ưu tiên theo hậu quả và số lần lặp.
9. Điều chưa đủ bằng chứng (skill nào sinh lỗi, hậu quả đo được bao nhiêu) thì đưa vào câu hỏi mở.

## 4. Mẫu đầu ra
```
## Tổng kết bài học: <sprint hoặc phase>
**Nguồn:** <ghi chú retro> · **Người tham gia (theo vai trò):** <danh sách vai> · **Giới hạn:** <ví dụ thiếu log lỗi trước>

### 1. Chủ đề
| # | Chủ đề | Giữ (tốt) | Đổi (chưa tốt) | Bằng chứng | Số lần nhắc |
|---|---|---|---|---|---|

### 2. Hành động
| ID | Hành động | Chủ đề | Vai chịu trách nhiệm | Hạn | Xong khi |
|---|---|---|---|---|---|

### 3. Lỗi AI lặp lại cần sửa skill
| ID | Lỗi AI | Loại lỗi | Xuất hiện ở (từ 2 nơi) | Hậu quả | Skill cần sửa | Đề xuất sửa (mục + nội dung) | Cách kiểm tra lại | Ưu tiên |
|---|---|---|---|---|---|---|---|---|

### 4. Lỗi AI mới thấy một lần (theo dõi)
| ID | Lỗi | Skill liên quan | Khi nào nâng lên "lặp lại" |
|---|---|---|---|

### Câu hỏi mở
1. <câu hỏi, ghi cần ai trả lời>
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Toàn bộ kết quả, kể cả trích dẫn, không còn tên người, chỉ còn vai trò?
- [ ] Mỗi chủ đề có ít nhất một bằng chứng trích từ ghi chú, và số lần nhắc khớp với số ghi chú cùng nhãn (Ý tưởng không cộng)?
- [ ] Mỗi hành động có vai chịu trách nhiệm (không phải tên), hạn và tiêu chí "xong khi" kiểm chứng được?
- [ ] Mỗi lỗi AI trong bảng 3 nêu từ hai nơi xuất hiện trở lên, dùng đúng slug skill có trong repo, và đề xuất nêu rõ quy tắc đã có ở skill đích cùng chỗ làm cứng (không lặp lại nội dung sẵn có)?
- [ ] Lỗi AI chỉ thấy một lần nằm ở bảng 4, không lẫn vào bảng 3?
- [ ] Lỗi quy trình hoặc yếu tố bên ngoài được tách khỏi lỗi AI, và mỗi đề xuất sửa skill có cách kiểm tra lại?

## 6. BA phải verify
- AI dễ gán lỗi cho sai skill khi một tài liệu do nhiều skill hoặc nhiều lần chạy tạo ra. Trainer xác nhận skill nguồn bằng cách xem lại phiên chạy hoặc đầu vào đã dùng.
- AI dễ coi một sự cố được nhắc hai lần là "lặp lại". Kiểm tra đó có thật là hai tài liệu hoặc hai lần khác nhau.
- Đề xuất sửa skill chưa được thử; chỉ coi là xong khi chạy lại và lỗi không còn. Lỗi có thể do đầu vào thiếu (ví dụ không đưa business rule cho AI) chứ không do skill.
- Số lần nhắc, mức ưu tiên và hạn là ước lượng của AI; BA hoặc PM chốt.
- Ghi chú retro bỏ sót ngữ cảnh bằng lời; chủ đề AI gom có thể thiếu điều quan trọng chưa ai ghi.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- **Ẩn danh tên người trong retro** (đồng nghiệp, stakeholder, khách hàng). Chỉ ghi vai trò và hiện tượng, không ghi ai sai. Tên nằm trong trích dẫn cũng thay bằng vai.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi hạn, số liệu, tên sprint không có nguồn trong ghi chú.
- Nhận xét nhạy cảm về cá nhân trong ghi chú thì bỏ hoặc trung hòa thành hiện tượng quy trình; không chép nguyên.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
