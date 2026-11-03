---
name: analyze-business-rules
description: Tách business rule từ chính sách và quy trình thành các rule nguyên tử, phân loại definition hay behaviour, rồi phát hiện rule mâu thuẫn, mơ hồ hoặc thiếu. Dùng khi BA có chính sách, mô tả quy trình hoặc ghi chú phỏng vấn chứa quy tắc cần chuẩn hóa, ví dụ "phân tích business rule", "tách rule từ chính sách", "tìm mâu thuẫn giữa các rule". Chỉ dùng cho việc tách và chuẩn hóa rule, không viết luồng. Không dùng khi cần viết hoặc đặc tả use case có chứa rule (dùng write-use-case-spec), khi cần AC (dùng write-user-story-and-ac), khi cần soát chất lượng cả tài liệu yêu cầu theo 5 tiêu chí (dùng pre-review-requirements), hoặc khi cần chuẩn hóa thuật ngữ (dùng build-glossary).
---

# Phân tích business rule (Business Rules Analysis – BABOK v3)

## 1. Mục đích
Business Rules Analysis là việc rút các quy tắc đang nằm rải rác trong chính sách, quy trình, lời kể của stakeholder thành những phát biểu ngắn, kiểm được, có nguồn và có chủ. Skill này chia rule làm hai loại: **definition** (rule định nghĩa: một khái niệm nghĩa là gì, được tính ra sao) và **behaviour** (rule hành vi: ai, khi nào, được hoặc phải hoặc không được làm gì). Sau khi tách, skill đối chiếu để thấy rule mâu thuẫn, mơ hồ hoặc thiếu trước khi chúng biến thành yêu cầu, use case, test. Skill không tự quyết rule nào đúng.

## 2. Đầu vào cần có
- Chính sách, mô tả quy trình hoặc ghi chú phỏng vấn có chứa quy tắc, kèm nguồn (ai nói, tài liệu nào).
- Danh sách rule đã có (BR-xx), nếu có, để đối chiếu. Tùy chọn.
- Danh sách yêu cầu hoặc use case liên quan (R-xx, UC-xx) để kiểm mâu thuẫn rule với yêu cầu. Tùy chọn.
- Tình huống BA đang băn khoăn (ví dụ "hai bản ghi khác nhau chút ít có coi là trùng không"). Tùy chọn.
- Người sở hữu rule, nếu biết. Tùy chọn.

Thiếu văn bản nguồn thì **hỏi lại người dùng trước khi làm**. Không tự bịa rule để lấp chỗ trống.

## 3. Các bước
1. Gạch mọi câu có tín hiệu rule (phải, không được, chỉ, nếu... thì, mỗi, ngưỡng, tối đa/tối thiểu, được duyệt bởi). Gợi ý tín hiệu và mẫu phát biểu nằm trong `references/rule-patterns.md`.
2. Tách thành rule nguyên tử: một phát biểu = một điều kiện + một hệ quả. Câu ghép thì tách, ghi rõ nguồn gốc ở cột Nguồn.
3. Chuẩn hóa mỗi rule thành một câu: definition viết "<Thuật ngữ> là <định nghĩa>"; behaviour viết "Nếu <điều kiện> thì <vai> <phải/không được/được> <hành động>".
4. Phân loại Definition hay Behaviour; với behaviour ghi thêm kiểu (Bắt buộc, Cấm, Cho phép, Điều kiện–hành động). Rule nằm sát ranh giới thì chọn một loại, ghi lý do ở cột Ghi chú để BA chốt.
5. Giữ mã rule đã có. Rule input chưa đánh mã thì gán mã tạm và gắn `[GIẢ ĐỊNH]`. Chủ sở hữu input không nêu thì ghi "chưa rõ".
6. Rule có nhiều mức hoặc ngưỡng thì giữ là một rule, ghi chú "rule bảng quyết định" và dựng bảng quyết định ở mục 2. Giá trị không có nguồn gắn `[GIẢ ĐỊNH]`.
7. Đối chiếu từng cặp rule và rule với yêu cầu. Tìm: mâu thuẫn trực tiếp, mâu thuẫn gián tiếp (cùng đúng chỉ khi có điều kiện ngầm), khoảng trống (tình huống không rule nào phủ), trùng lặp, và tiêu chí so khớp chưa rõ (ví dụ "trùng", "quá hạn"). Đặt mã GAP-nn cho chỗ mơ hồ hoặc thiếu, X-nn cho mâu thuẫn, TP-n cho cặp dữ liệu thử. Mỗi phát hiện kèm một tình huống cụ thể làm lộ vấn đề.
8. Mỗi phát hiện nêu từ hai phương án giải quyết trở lên và ai quyết. Không chọn hộ.
9. Gom thuật ngữ cần định nghĩa (chuyển build-glossary) và nêu rule nào đã sẵn sàng đưa sang use case hoặc AC.

## 4. Mẫu đầu ra
```
## Phân tích business rule: <chủ đề>
**Nguồn:** <tài liệu> · **Phạm vi:** <rule nào> · **Giới hạn:** <ví dụ thiếu văn bản X>
<ghi chú mã tạm, nếu có>

### 1. Bảng rule
| Mã | Phát biểu rule | Loại | Kiểu (nếu Behaviour) | Nguồn | Chủ sở hữu | Ghi chú |
|---|---|---|---|---|---|---|

### 2. Bảng quyết định
<chỉ khi có rule nhiều mức; nếu không, ghi "Không có">

### 3. Mâu thuẫn giữa các rule
| ID | Vế A | Vế B | Mức mâu thuẫn | Tình huống làm lộ | Phương án giải quyết | Ai quyết |
|---|---|---|---|---|---|---|

### 4. Rule mơ hồ và khoảng trống
| ID | Rule | Vấn đề | Mức độ | Tình huống minh họa | Cần làm rõ với |
|---|---|---|---|---|---|
<bảng thử trên dữ liệu ví dụ, nếu BA nêu tình huống cần thử>

### 5. Thuật ngữ cần định nghĩa
- <thuật ngữ>: <vì sao cần>
**Rule sẵn sàng chuyển tiếp** (write-use-case-spec, write-user-story-and-ac): <mã rule, hoặc "chưa có">

### Câu hỏi mở
1. <câu hỏi, ghi cần ai trả lời>
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi rule trong bảng là nguyên tử, viết một câu, và truy được về nguồn trong đầu vào?
- [ ] Mỗi rule có đúng một loại (Definition hoặc Behaviour), và rule sát ranh giới có ghi lý do?
- [ ] Mỗi mâu thuẫn nêu đủ hai vế, dẫn đúng mã và có tình huống cụ thể minh họa?
- [ ] Mỗi phát hiện có ít nhất hai phương án, ghi rõ ai quyết, và không chọn hộ?
- [ ] Mọi ngưỡng, số liệu, mã tạm không có trong nguồn đều gắn `[GIẢ ĐỊNH]`?
- [ ] Tiêu chí so khớp chưa rõ (trùng, quá hạn) được đưa thành phát hiện hoặc câu hỏi mở, không tự định nghĩa?

## 6. BA phải verify
- AI hay thêm rule "hợp lý" không có trong nguồn (thời hạn, ngoại lệ, quy tắc làm tròn). Đối chiếu từng rule với nguồn.
- Ranh giới Definition và Behaviour là chỗ dễ tranh luận; BA chốt, nhất là rule thời hạn và ngưỡng.
- Một "mâu thuẫn" có thể chỉ là hai rule áp cho hai vai khác nhau. Xác nhận với chủ sở hữu rule trước khi kết luận.
- AI hay bỏ sót khoảng trống ở biên: đúng ngưỡng, hết hạn, đang chờ duyệt, hai sự kiện xảy ra cùng lúc.
- Cột chủ sở hữu và mã tạm do AI gán, không phải sự thật.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Rule về chiết khấu, hạn mức, công nợ là thông tin nhạy cảm của doanh nghiệp: ví dụ tình huống chỉ dùng giá trị bịa, không dùng tên khách hàng hoặc con số thật.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
