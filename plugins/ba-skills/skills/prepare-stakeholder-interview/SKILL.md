---
name: prepare-stakeholder-interview
description: Soạn bộ câu hỏi phỏng vấn một stakeholder (câu chính, câu đào sâu) kèm khung tóm tắt biên bản, từ mục tiêu buổi phỏng vấn và vai của người được phỏng vấn. Dùng khi BA chuẩn bị gặp 1–1 hoặc nhóm nhỏ, hoặc có ghi chú sau buổi cần gọn lại thành biên bản, ví dụ "soạn câu hỏi phỏng vấn", "chuẩn bị buổi phỏng vấn chị Hạnh", "điền khung biên bản từ ghi chú thô". Không dùng khi cần họp nhiều bên để chốt quyết định (dùng plan-requirements-workshop), khảo sát số đông (dùng design-survey-and-analyze), chốt thuật ngữ từ biên bản (dùng build-glossary) hoặc đọc tài liệu viết sẵn (dùng analyze-source-documents).
---

# Phỏng vấn stakeholder (Interviews)

## 1. Mục đích
Interviews là cách BA hỏi trực tiếp một người hoặc một nhóm nhỏ, theo kế hoạch, để lấy ra thông tin mà tài liệu không có: cách làm thật, ngoại lệ, quy tắc ngầm, mong muốn. Chất lượng đến từ việc hiểu người được hỏi trước khi hỏi, hỏi mở rồi đào sâu bằng ví dụ có thật, và ghi lại ngay sau buổi để người đó xác nhận. Skill này chuẩn bị phần "trước" (câu hỏi) và phần "sau" (khung biên bản), không thay BA ngồi nghe.

## 2. Đầu vào cần có
- Mục tiêu buổi phỏng vấn: cần biết điều gì sau buổi này.
- Người được phỏng vấn: tên, vai, và những gì đã biết về họ (hay nói nhanh, ngại điều gì, quan tâm điều gì).
- Thời lượng và hình thức (1–1, họp online) (tùy chọn; không có thì gắn `[GIẢ ĐỊNH]`).
- Yêu cầu hoặc rule đã biết liên quan (R*, BR-*) để câu hỏi trỏ về đúng chỗ (tùy chọn).
- Ghi chú thô sau buổi phỏng vấn (tùy chọn; có thì điền khung biên bản).

Thiếu mục tiêu hoặc vai người được phỏng vấn thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Viết lại mục tiêu thành 1–3 điều "phải biết sau buổi".
2. Đọc vai người được hỏi: họ nắm gì, ngại gì, cách nói chuyện. Chỉ dùng thông tin có trong đầu vào.
3. Xếp chủ đề theo dòng: mở đầu, hiện trạng (kể một trường hợp gần nhất), ngoại lệ và nỗi đau, rule, mong muốn, chốt.
4. Mỗi chủ đề viết 1 câu chính mở và 1–3 câu đào sâu. Tránh câu dẫn dắt, câu kép, câu chỉ có/không. Xem `references/question-patterns.md`.
5. Gắn mã Q và mục đích cho từng câu, trỏ về R*/BR-*/UC cần làm rõ. Câu không trỏ được thì gắn "khám phá" hoặc bỏ.
6. Lọc "thuật ngữ cần chốt": từ người đó có thể dùng khác nghĩa với người khác. Đây là đầu vào cho build-glossary.
7. Chia thời gian theo chủ đề; chủ đề quan trọng nhất ở giữa buổi, không để cuối.
8. Dựng khung tóm tắt biên bản. Nếu có ghi chú sau buổi, điền khung: chỉ ghi điều được nói, suy luận của BA gắn `[GIẢ ĐỊNH]`.
9. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Phỏng vấn: <tên, vai>
**Mục tiêu:** ... · **Thời lượng:** ... · **Hình thức:** ...
**Phải biết sau buổi:** 1) ... 2) ...
**Lưu ý cách hỏi:** <3–4 gạch đầu dòng ràng buộc quy trình; không ghi nhận xét tính cách>

### Bộ câu hỏi
| Mã | Nhóm (phút) | Câu hỏi chính | Câu đào sâu | Mục đích (trỏ về) |
|---|---|---|---|---|

Ghi phút ở dòng đầu của nhóm, các dòng sau chỉ ghi chữ cái nhóm. Mỗi câu chính chỉ một ý; ý thứ hai chuyển sang cột đào sâu.

### Thuật ngữ cần chốt (đầu vào cho build-glossary)
| Thuật ngữ | Vì sao cần chốt |
|---|---|

### Khung tóm tắt biên bản (điền sau buổi)
| Mã Q | Chủ đề | Điều đã nghe | Loại | Rule/nhu cầu liên quan | Cần xác nhận |
|---|---|---|---|---|---|
Loại: Fact · Rule · Nhu cầu · Ý kiến.
**Việc sau buổi:** gửi biên bản cho người được hỏi xác nhận trong <thời hạn>.

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi câu chính là câu mở và không gợi sẵn đáp án mong muốn?
- [ ] Mỗi câu có mã Q và trỏ về một R*/BR-*/UC, hoặc ghi rõ "khám phá"?
- [ ] Có ít nhất một câu yêu cầu kể trường hợp thật gần nhất thay vì hỏi chung chung?
- [ ] Tổng thời gian các nhóm khớp thời lượng buổi?
- [ ] Rule đang giả định (ví dụ BR-D3) được hỏi như câu mở, không đưa số như sự thật?
- [ ] Cột "Loại" phân biệt được điều đã thấy (Fact) với ý kiến cá nhân?

## 6. BA phải verify
- AI hay viết câu hỏi dẫn dắt hoặc câu hỏi kép ("A và B thì sao?"): đọc lại từng câu.
- AI hay đưa nhận xét tính cách vào tài liệu chia sẻ; chỉ giữ ràng buộc quy trình, hồ sơ tính cách (nếu cần) để riêng cho BA.
- Biên bản điền từ ghi chú thô dễ biến ý kiến thành rule; BA rà cột "Loại" và gửi người được hỏi xác nhận.
- Số thời lượng mỗi nhóm chỉ là gợi ý; BA điều chỉnh theo độ quan trọng thực tế.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Biên bản phỏng vấn gắn với cá nhân: ghi vai thay cho tên khi chia sẻ rộng; xin phép trước khi ghi âm.
- Không đưa nhận xét tính cách người được hỏi vào bản chia sẻ; nêu ràng buộc quy trình thay thế.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
