---
name: analyze-source-documents
description: Đọc một tài liệu nguồn đã ẩn danh (quy trình, hướng dẫn nội bộ, biểu mẫu, hợp đồng mẫu) rồi trích tóm tắt, rule, thuật ngữ và các câu hỏi xuất phát từ chỗ thiếu hoặc mâu thuẫn. Dùng khi nguồn là tài liệu viết sẵn (không phải biên bản phỏng vấn) và BA cần hiểu hiện trạng trước khi gặp người, ví dụ "phân tích tài liệu này", "trích rule từ quy trình", "đọc file hướng dẫn nội bộ". Không dùng khi cần hỏi người (dùng prepare-stakeholder-interview), đã có biên bản và chỉ cần chốt thuật ngữ (dùng build-glossary), cần so sánh nhiều đối tượng theo tiêu chí (dùng research-benchmark) hoặc cần vẽ cấu trúc ý (dùng build-mind-map).
---

# Phân tích tài liệu nguồn (Document Analysis)

## 1. Mục đích
Document Analysis là việc đọc có chủ đích các tài liệu đang có để rút ra thông tin giúp hiểu bối cảnh và yêu cầu: quy trình hiện hành, rule, dữ liệu, thuật ngữ. Tài liệu rẻ để lấy và không đòi thời gian của người khác, nhưng thường cũ, không đầy đủ, và ghi cách làm trên giấy chứ không phải cách làm thật. Vì vậy mỗi điều trích ra phải có nguồn đoạn nào, được đối chiếu với những gì đã biết, và chỗ thiếu hay mâu thuẫn phải biến thành câu hỏi cho người thật.

## 2. Đầu vào cần có
- Nội dung tài liệu đã ẩn danh (dán văn bản, có số đoạn nếu được).
- Mục tiêu đọc: đang tìm gì (rule? quy trình? dữ liệu?).
- Thông tin nền đã biết để đối chiếu (R*, BR-*, UC) (tùy chọn, nên có).
- Thông tin về tài liệu: chủ sở hữu, ngày, phiên bản (tùy chọn; thiếu thì ghi "chưa rõ").

Thiếu nội dung tài liệu hoặc tài liệu chưa ẩn danh thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Ghi lại loại tài liệu, chủ sở hữu, ngày, độ tin cậy; nếu thiếu thì đánh dấu "chưa rõ" và hạ độ tin cậy.
2. Đọc một lượt, đánh số đoạn (§1, §2, ...) để mọi điều trích đều có nguồn.
3. Tóm tắt tối đa 5 câu: tài liệu nói về gì, ai dùng, phạm vi.
4. Trích rule: mỗi rule một dòng, diễn đạt lại ngắn, ghi đoạn nguồn, đánh giá độ rõ (Rõ/Mơ hồ).
5. Đối chiếu từng rule với thông tin nền: Khớp, Gần khớp, Mâu thuẫn, hoặc Mới. Không tự chọn bên đúng khi mâu thuẫn.
6. Trích thuật ngữ và cách tài liệu dùng (kể cả từ dùng mà không định nghĩa).
7. Liệt kê chỗ thiếu, mơ hồ, mâu thuẫn, mỗi chỗ ghi người có thể trả lời.
8. Đổi mỗi chỗ thiếu thành một câu hỏi cụ thể. Xem `references/extraction-checklist.md`.
9. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Phân tích tài liệu: <tên>
**Loại / chủ sở hữu / ngày:** ... · **Độ tin cậy:** <Cao/Trung bình/Thấp, lý do> · **Mục tiêu đọc:** ...

### Tóm tắt
<tối đa 5 câu>

### Rule trích xuất
| Mã | Rule (diễn đạt lại) | Nguồn | Đối chiếu | Độ rõ |
|---|---|---|---|---|
Mã tạm RT-xx. Đối chiếu: = Khớp mã đã biết · ≈ Gần khớp, cần xác nhận · ≠ Mâu thuẫn · Mới.

### Thuật ngữ
| Thuật ngữ | Cách tài liệu dùng | Nguồn | Ghi chú |
|---|---|---|---|

### Mâu thuẫn và chỗ thiếu
| Mã | Loại | Mô tả | Nguồn | Hỏi ai |
|---|---|---|---|---|
Mã GAP-01, GAP-02, ... Loại: Mâu thuẫn · Thiếu · Mơ hồ.

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi rule và thuật ngữ có đoạn nguồn để tra lại?
- [ ] Mỗi rule đã đối chiếu với thông tin nền, mâu thuẫn được nêu mà không chọn bên đúng?
- [ ] Phân biệt điều tài liệu nói rõ với điều AI suy ra (suy ra thì gắn `[GIẢ ĐỊNH]`)?
- [ ] Mỗi chỗ thiếu hoặc mâu thuẫn đều thành một câu hỏi có người trả lời?
- [ ] Độ tin cậy tài liệu được nêu cùng lý do (ngày, chủ sở hữu, bản nháp hay bản chính thức)?
- [ ] Không có thông tin định danh thật nào còn sót trong phần trích?

## 6. BA phải verify
- AI hay biến "khoảng", "thường", "đôi khi" thành rule cứng; BA rà cột "Độ rõ".
- Tài liệu mô tả cách làm trên giấy; cách làm thật có thể khác. Phải hỏi người dùng thật.
- AI dễ nối hai đoạn rời nhau thành một rule; BA mở lại đoạn nguồn kiểm tra.
- Đối chiếu "Khớp" chỉ là khớp về chữ; BA kiểm có cùng nghĩa với rule đã biết không.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Tài liệu hợp đồng, bảng giá, công nợ, danh sách khách: chỉ đưa vào bản đã thay tên, số tiền, mã bằng giá trị giả; từ chối xử lý bản còn dữ liệu thật.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
