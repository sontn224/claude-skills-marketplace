---
name: facilitate-brainstorming
description: Hỗ trợ một phiên brainstorming bằng cách ghi nhận ý của team, mở rộng thêm ý từ nhiều góc nhìn, gom nhóm và chấm điểm đề xuất để team chọn. Dùng khi cần nhiều phương án cho một vấn đề mở hoặc cần dọn một đống ý rời rạc, ví dụ "brainstorm ý tưởng", "gom nhóm và chấm điểm danh sách ý tưởng của team", "mở rộng danh sách ý của team". Không dùng khi cần các bên có mặt cùng chốt rule hay quyết định (dùng plan-requirements-workshop), cần thu ý kiến từ đông người (dùng design-survey-and-analyze) hoặc cần vẽ cấu trúc ý (dùng build-mind-map).
---

# Brainstorming (Brainstorming)

## 1. Mục đích
Brainstorming là cách cả nhóm sinh ra thật nhiều ý tưởng cho một vấn đề trong thời gian ngắn, rồi mới lọc và chọn. Giá trị đến từ việc tách hai pha: pha sinh ý không chấm điểm, không bác bỏ; pha sau mới gom nhóm và đánh giá theo tiêu chí chung. Làm gộp hai pha khiến người ít nói im đi và ý lạ bị loại sớm. Skill này hỗ trợ cả hai pha trên văn bản: ghi ý của team, bổ sung ý ở góc team chưa nghĩ tới, gom nhóm, và đề xuất điểm để team chấm lại.

## 2. Đầu vào cần có
- Chủ đề, tốt nhất viết dạng câu hỏi "Làm sao để ...?" kèm kết quả mong muốn.
- Ý của team đã có (danh sách thô, có thể trùng và lộn xộn).
- Ràng buộc: phạm vi dự án, thời gian, ngân sách, chính sách đã chốt (tùy chọn, nên có để cờ phạm vi đúng).
- Tiêu chí chấm của team (tùy chọn; không có thì dùng Tác động và Khả thi, xem `references/scoring.md`).

Thiếu chủ đề hoặc danh sách ý ban đầu thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Viết lại chủ đề thành câu hỏi mở và nêu ràng buộc.
2. Ghi ý của team nguyên văn, đánh mã B1, B2, ...; chỉ gộp khi hai ý cùng nghĩa và ghi mã gốc. Không loại ý nào ở bước này.
3. Mở rộng: thêm ý từ các góc team chưa chạm (người dùng, quy trình, chính sách, kỹ thuật, truyền thông, rủi ro). Gắn nguồn "AI đề xuất" và đánh mã tiếp theo.
4. Gom nhóm theo bản chất ý, không theo người nói; mỗi nhóm có tên và một câu mô tả.
5. Chấm điểm đề xuất: Tác động (1–5), Khả thi (1–5, 5 = dễ), Điểm = Tác động × Khả thi; ghi lý do ngắn.
6. Gắn cờ phạm vi cho từng ý: Trong scope · Vận hành · Chính sách (cần người quyết) · Ngoài scope. Ý chạm phạm vi hoặc chính sách thì không đưa vào backlog trực tiếp.
7. Chọn tối đa 5 ý ưu tiên (mỗi dòng một ý; ý có mốc thời gian riêng ghi ở dòng "mốc riêng", không đếm vào 5); ý hoãn hoặc loại phải có lý do rõ (không loại chỉ vì điểm thấp).
8. Nhắc rõ điểm là đề xuất, team chấm lại bằng cách bỏ phiếu.
9. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Brainstorming: <chủ đề>
**Câu hỏi chủ đề:** Làm sao để ...? · **Ràng buộc:** ... · **Số ý:** <n> của team, <m> AI đề xuất

### Danh sách ý (đã mở rộng)
| Mã | Ý | Nguồn | Ghi chú |
|---|---|---|---|

### Gom nhóm
| Nhóm | Ý (mã) | Ý nghĩa của nhóm |
|---|---|---|

### Chấm điểm đề xuất
| Mã | Tác động | Khả thi | Điểm | Phạm vi | Lý do |
|---|---|---|---|---|---|

### Đề xuất ưu tiên
1. ...

### Ý hoãn hoặc loại
| Mã | Quyết định | Lý do |
|---|---|---|

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mọi ý của team đều còn trong danh sách (không bị bỏ hay viết lại sai nghĩa)?
- [ ] Ý AI đề xuất được gắn nguồn riêng và không nhiều hơn ý của team?
- [ ] Mỗi ý thuộc đúng một nhóm và tên nhóm mô tả bản chất, không phải tên người?
- [ ] Điểm có lý do ngắn, và Điểm = Tác động × Khả thi tính đúng?
- [ ] Ý chạm phạm vi hoặc chính sách có cờ riêng và có người quyết trong "Câu hỏi mở"?
- [ ] Ý bị hoãn hoặc loại đều có lý do, không loại thầm?

## 6. BA phải verify
- AI hay chấm điểm cao cho ý nghe hay nhưng khó làm; team phải chấm lại, đừng dùng điểm AI làm quyết định.
- Ý AI đề xuất có thể chạm chính sách hoặc phạm vi mà AI không biết; BA kiểm cờ phạm vi.
- Gom nhóm có thể làm mất ý lạ lọt giữa hai nhóm; BA đọc lại ý nào đặt sai chỗ.
- Số liệu trong lý do (chi phí, thời gian) nếu không có nguồn là giả định; BA đừng sao chép vào kế hoạch.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Ý của team ghi theo nhóm, không gắn tên người nói để giữ tính ẩn danh của pha sinh ý.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
