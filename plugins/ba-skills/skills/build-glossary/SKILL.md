---
name: build-glossary
description: Gom thuật ngữ nghiệp vụ từ tài liệu hoặc biên bản thành bảng có định nghĩa, nguồn, đồng nghĩa và nhãn độ chắc của nguồn, đồng thời chỉ ra chỗ một từ bị dùng với nhiều nghĩa. Dùng khi đã có biên bản hoặc ghi chú từ một hay nhiều nguồn và cần chốt tên chuẩn cho các thuật ngữ trước khi viết use case hay user story, ví dụ "lập bảng thuật ngữ", "chốt định nghĩa các từ này", "làm glossary từ biên bản". Không dùng khi chưa có nguồn nào (dùng prepare-stakeholder-interview để hỏi trước), cần trích rule và câu hỏi từ tài liệu viết sẵn (dùng analyze-source-documents) hoặc cần vẽ cây ý (dùng build-mind-map).
---

# Bảng thuật ngữ (Glossary)

## 1. Mục đích
Glossary là danh mục các thuật ngữ quan trọng của một lĩnh vực hay dự án, mỗi từ có một nghĩa được các bên thống nhất. Nó giảm hiểu nhầm giữa người nghiệp vụ, BA, developer và tester, nhất là khi cùng một từ được dùng cho hai việc hoặc hai từ chỉ một việc. Glossary đứng giữa phỏng vấn và đặc tả: nó lấy từ ngữ thật của stakeholder, chốt tên chuẩn, rồi use case và user story dùng đúng tên đó. Định nghĩa chỉ có giá trị khi có nguồn và người nắm nghiệp vụ xác nhận.

## 2. Đầu vào cần có
- Tài liệu hoặc biên bản đã ẩn danh (ưu tiên biên bản của prepare-stakeholder-interview: dùng được cột Q, cột Loại và bảng "Thuật ngữ cần chốt").
- Bối cảnh ngắn về dự án hoặc lĩnh vực để hiểu từ chuyên môn (tùy chọn).
- Bảng thuật ngữ đã có (tùy chọn; có thì bổ sung, không viết lại).

Thiếu nguồn thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Xác định phạm vi và các nguồn; mỗi nguồn có mã để dẫn (Q2, §4, ...).
2. Quét cụm từ nghiệp vụ lặp lại, từ viết tắt, tên vai, tên trạng thái, tên tài liệu. Bỏ từ thông dụng mà ai cũng hiểu như nhau.
3. Với mỗi thuật ngữ, chọn tên chuẩn theo cách người nghiệp vụ hay dùng, viết định nghĩa 1–2 câu, không định nghĩa vòng quanh chính từ đó.
4. Ghi đồng nghĩa đang được dùng và từ nên tránh.
5. Ghi nguồn và nơi dùng (R*, BR-*, UC-*) để truy vết.
6. Đánh nhãn độ chắc, đúng ba giá trị: `Có nguồn` · `Cần xác minh` · `[GIẢ ĐỊNH]`. Nếu nguồn là biên bản phỏng vấn, ánh xạ từ cột Loại: Fact hoặc Rule do người có thẩm quyền nói → `Có nguồn`; Ý kiến, hoặc chỉ một người nói, hoặc lời nói mơ hồ → `Cần xác minh`; Nhu cầu → không dùng làm định nghĩa (chuyển sang rule hoặc yêu cầu); BA tự suy → `[GIẢ ĐỊNH]`.
7. Tìm xung đột: một từ nhiều nghĩa, nhiều từ một nghĩa, cùng từ khác phòng ban. Đề xuất tên chuẩn nhưng để chủ nghiệp vụ chốt.
8. Tách riêng thuật ngữ chưa đủ nguồn; không viết định nghĩa cho chúng.
9. Gợi ý chuyển tiếp: thuật ngữ nào thành actor, trạng thái, dữ liệu, rule trong Use Case và User Story. Xem `references/glossary-conventions.md` nếu cần quy ước.
10. Kết bằng "Câu hỏi mở".

## 4. Mẫu đầu ra
```
## Bảng thuật ngữ: <phạm vi>
**Nguồn:** ... · **Số thuật ngữ:** <n> · **Nhãn:** Có nguồn · Cần xác minh · [GIẢ ĐỊNH]

### Bảng thuật ngữ
| Thuật ngữ | Định nghĩa | Đồng nghĩa / tránh dùng | Nguồn | Nhãn | Dùng ở |
|---|---|---|---|---|---|

### Xung đột cách dùng
| Mã | Vấn đề | Đề xuất tên chuẩn | Ai chốt |
|---|---|---|---|

### Thuật ngữ chưa đủ nguồn để định nghĩa
| Thuật ngữ | Đã biết gì | Cần hỏi gì |
|---|---|---|

### Gợi ý chuyển tiếp
- <thuật ngữ> → <actor / trạng thái / dữ liệu / rule trong Use Case, User Story>

### Câu hỏi mở
1. <câu hỏi> (cần: <ai trả lời>)
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi định nghĩa có nguồn dẫn lại được và không định nghĩa vòng?
- [ ] Mỗi thuật ngữ chỉ có một tên chuẩn; các tên khác nằm ở cột đồng nghĩa hoặc tránh dùng?
- [ ] Từ dùng cho nhiều nghĩa (đồng âm khác nghĩa) đã được liệt kê ở "Xung đột cách dùng"?
- [ ] Thuật ngữ chưa đủ nguồn được tách riêng, không có định nghĩa bịa?
- [ ] Nhãn `Có nguồn` chỉ dùng khi nguồn nói trực tiếp và không mâu thuẫn nguồn khác?
- [ ] Tên chuẩn dùng nhất quán trong toàn bảng (kể cả khi nhắc ở cột định nghĩa)?

## 6. BA phải verify
- AI hay viết định nghĩa "hợp lý" từ kiến thức chung thay vì cách công ty này dùng; BA đối chiếu với nguồn.
- Tên chuẩn do AI đề xuất chưa phải quyết định; chủ nghiệp vụ phải chốt.
- Hai từ giống nhau ở bề mặt có thể khác nghĩa theo phòng ban; BA hỏi lại người dùng khi có nghi ngờ.
- Định nghĩa bằng con số hay thời hạn (ví dụ thời hạn bảo hộ) phải khớp rule đã xác nhận, không chép từ một lời nói.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Ví dụ minh họa trong định nghĩa dùng tên giả hoặc vai, không dùng tên khách, mã hợp đồng, số tiền thật.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
