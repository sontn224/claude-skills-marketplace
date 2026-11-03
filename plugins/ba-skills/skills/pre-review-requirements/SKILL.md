---
name: pre-review-requirements
description: Rà soát sơ bộ một tài liệu yêu cầu và trả bảng lỗi theo 5 tiêu chí (đủ, rõ, nhất quán, kiểm chứng được, truy vết được), mỗi lỗi có vị trí, mức độ và gợi ý sửa. Dùng khi BA có bản nháp yêu cầu, spec hoặc danh sách user story cần lọc lỗi trước buổi review chính thức, ví dụ "review yêu cầu", "rà soát tài liệu yêu cầu", "lọc lỗi trước buổi review". Không dùng khi cần viết hoặc viết lại yêu cầu (dùng write-user-story-and-ac hoặc write-use-case-spec), khi cần biến một yêu cầu phi chức năng mơ hồ thành chỉ số đo được (dùng write-nfr), khi chỉ cần tách và chuẩn hóa business rule (dùng analyze-business-rules), hoặc khi muốn thay buổi review có stakeholder.
---

# Rà soát sơ bộ yêu cầu (Reviews – BABOK v3)

## 1. Mục đích
Reviews là việc kiểm tra một work product để tìm lỗi và khoảng trống trước khi người khác dựa vào nó. Ở đây work product là tài liệu yêu cầu, và skill làm vòng lọc đầu (pre-review): AI đọc nhanh, gắn lỗi theo năm tiêu chí chất lượng yêu cầu, để buổi review chính thức với người thật dành thời gian cho quyết định chứ không phải cho lỗi câu chữ. Skill chỉ chỉ ra lỗi và gợi ý hướng xử lý. Việc sửa, việc chốt mức độ và việc quyết định thuộc về BA.

## 2. Đầu vào cần có
- Tài liệu yêu cầu cần review, mỗi yêu cầu có mã định danh (R1, US-xx, ...). Chưa có mã thì hỏi BA hoặc đánh số tạm và ghi rõ là số tạm.
- Phạm vi dự án: in scope, out of scope.
- Tài liệu tham chiếu để đối chiếu nhất quán (business rule, glossary, yêu cầu khác). Tùy chọn nhưng nên có.
- Danh sách tính năng, use case hoặc user story để kiểm truy vết. Tùy chọn; thiếu thì chỉ kiểm "yêu cầu có nguồn không".

Thiếu tài liệu hoặc phạm vi thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Chốt đối tượng review: tên tài liệu, phiên bản, tập mã yêu cầu, và các tài liệu tham chiếu dùng để so.
2. Đọc hết một lượt, lập danh sách mã yêu cầu. Yêu cầu thiếu mã, thiếu nguồn thì ghi lỗi truy vết.
3. Duyệt từng yêu cầu qua 5 tiêu chí. Câu hỏi chi tiết, từ mơ hồ thường gặp và định nghĩa mức độ nằm trong `references/review-criteria.md`.
4. Đối chiếu chéo: yêu cầu với yêu cầu, với phạm vi, với business rule (nhất quán); với tính năng và use case, cả hai chiều (truy vết).
5. Ghi mỗi lỗi một dòng: vị trí (mã yêu cầu hoặc số dòng/mục), tiêu chí, vấn đề kèm trích đoạn ngắn, mức độ, gợi ý sửa dạng hướng hoặc câu hỏi. Không viết lại yêu cầu thay BA.
6. Gộp các lỗi cùng một gốc thành một dòng. Không bịa lỗi cho đủ số lượng; yêu cầu không thấy lỗi thì ghi "chưa phát hiện lỗi".
7. Gán mức độ Cao / Trung bình / Thấp theo định nghĩa trong references, sắp bảng theo mức độ giảm dần, rồi đếm theo tiêu chí.
8. Ghi riêng các việc phát hiện nhưng nằm ngoài review (ví dụ cần chạy analyze-business-rules hoặc write-nfr) và các câu hỏi mở.

## 4. Mẫu đầu ra
```
## Pre-review: <tên tài liệu, phiên bản>
**Phạm vi:** <yêu cầu nào> · **Đối chiếu với:** <tài liệu tham chiếu> · **Giới hạn:** <ví dụ thiếu tài liệu X>

### Tóm tắt
| Tiêu chí | Cao | Trung bình | Thấp | Tổng |
|---|---|---|---|---|
| Đủ / Rõ / Nhất quán / Kiểm chứng được / Truy vết được | n | n | n | n |

### Bảng lỗi
| ID | Vị trí | Tiêu chí | Vấn đề | Mức độ | Gợi ý sửa |
|---|---|---|---|---|---|
| L-01 | <mã yêu cầu / dòng> | <1 trong 5> | <mô tả + trích đoạn ngắn> | Cao/Trung bình/Thấp | <hướng hoặc câu hỏi, không viết lại thay BA> |

### Yêu cầu chưa phát hiện lỗi
<danh sách mã, kèm lưu ý "chưa phát hiện lỗi" không có nghĩa là đúng>

### Việc ngoài phạm vi review
- <việc, skill nên dùng>

### Câu hỏi mở
1. <câu hỏi, ghi cần ai trả lời>
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi dòng lỗi có đủ vị trí cụ thể, tiêu chí, mức độ và gợi ý sửa?
- [ ] Gợi ý sửa chỉ là hướng hoặc câu hỏi, không viết lại yêu cầu thay BA, và mọi con số trong gợi ý đều gắn `[GIẢ ĐỊNH]`?
- [ ] Mọi mã yêu cầu trong đầu vào đều xuất hiện trong bảng lỗi hoặc trong danh sách "chưa phát hiện lỗi"?
- [ ] Mỗi lỗi "Nhất quán" nêu rõ hai vế và dẫn đúng mã của cả hai?
- [ ] Bảng tóm tắt khớp số dòng trong bảng lỗi, tổng theo mức độ và theo tiêu chí đều khớp?
- [ ] Mỗi lỗi mức Cao có nêu hậu quả nếu để nguyên (chặn thiết kế, không nghiệm thu được, tranh chấp phạm vi)?

## 6. BA phải verify
- Lỗi "Nhất quán" do AI báo có thể là hiểu sai vai hoặc ngữ cảnh; kiểm lại với người sở hữu rule trước khi đưa vào review.
- AI không biết những thỏa thuận miệng chưa vào tài liệu nên có thể báo "thiếu" cho thứ đã được chốt.
- Mức độ AI gán chỉ là gợi ý; BA chốt theo rủi ro thật của dự án.
- "Chưa phát hiện lỗi" phụ thuộc tài liệu tham chiếu được đưa vào; thiếu tham chiếu thì bỏ sót.
- Lỗi truy vết phụ thuộc việc có đưa danh sách tính năng hay không.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Trích đoạn trong bảng lỗi chỉ đủ ngắn để định vị. Tài liệu có giá, hợp đồng, công nợ thật thì yêu cầu ẩn danh trước, không chép lại vào bảng.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
