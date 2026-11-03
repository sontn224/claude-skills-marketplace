---
name: write-user-story-and-ac
description: Chuyển use case spec thành các user story theo INVEST, mỗi story kèm Acceptance Criteria dạng Given/When/Then (happy path, nhánh lỗi, nhánh biên) và truy vết về mã luồng của use case. Dùng khi đã có use case spec và cần backlog sẵn sàng cho sprint, ví dụ "viết user story", "viết acceptance criteria", "tách story từ use case". Không dùng khi chưa có spec (dùng write-use-case-spec), khi cần yêu cầu phi chức năng như hiệu năng, bảo mật (dùng write-nfr), hoặc khi cần mô tả màn hình (dùng generate-prototype-screens).
---

# Viết User Story và Acceptance Criteria (User Stories · Acceptance and Evaluation Criteria)

## 1. Mục đích
User story ghi một nhu cầu nhỏ, đủ để team ước lượng và làm trong một sprint, theo góc nhìn của người dùng: ai cần gì và để làm gì. Acceptance Criteria (AC) là các điều kiện kiểm chứng được, cho biết story đã làm đúng hay chưa. Use case spec mô tả đầy đủ các luồng nhưng quá lớn để giao việc. Skill này cắt spec thành story nhỏ, và gắn cho mỗi story các AC trỏ ngược về mã luồng gốc (main, A1, E2...) để không rơi mất nhánh lỗi. Story chưa có AC thì chưa xong, nên hai technique dùng chung một skill.

## 2. Đầu vào cần có
- Use case spec (đầu ra của `write-use-case-spec`): actor, precondition, postcondition, main flow, các luồng có mã A1, A2, E1, E2...
- Business rule liên quan, kèm ngưỡng và mã BR (ví dụ BR-C1); rule chưa có mã thì ghi rõ `[GIẢ ĐỊNH]` và đưa vào Câu hỏi mở.
- Các NFR liên quan từ `write-nfr` (mã NFR-xx) (tùy chọn); không có thì AC không tự đặt chỉ số hiệu năng (xem bước 6).
- Tên trạng thái và thuật ngữ đang dùng (lấy từ spec hoặc glossary) (tùy chọn).
- Phạm vi lần này: cả use case hay một vài luồng (tùy chọn; mặc định là cả use case).

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Spec chưa đánh mã luồng, hoặc người dùng chỉ có yêu cầu thô (R1...R12) thì dừng lại và gợi ý chạy `write-use-case-spec` trước. Không tự bịa luồng.

## 3. Các bước
1. Liệt kê toàn bộ luồng trong spec (main, alternative, exception) và mọi business rule có ngưỡng.
2. Cắt story theo quy tắc cố định, không cắt theo tầng kỹ thuật: một story cho main flow (kèm exception nghiệp vụ như E1, E2); một story cho mỗi alternative; một story chung cho nhóm lỗi hạ tầng (hệ thống ngoài không phản hồi, mất mạng); bước của vai khác (người duyệt) là story riêng. Xem `references/invest-checklist.md`.
3. Viết câu story: Là `<vai>`, tôi muốn `<việc>`, để `<giá trị>`. Vai lấy từ actor trong spec.
4. Kiểm từng story theo 6 tiêu chí INVEST. Story không đạt thì tách hoặc sửa, không bỏ qua.
5. Viết AC cho mỗi story theo Given/When/Then: một happy path, mỗi exception có ít nhất một AC lỗi, mỗi alternative có ít nhất một AC, và nhánh biên cho mọi ngưỡng (dưới, đúng, trên) hoặc giá trị rỗng, bằng 0, tối đa. Xem `references/ac-patterns.md`.
6. Mỗi AC đúng một When; mọi hành động đầu vào khác chuyển vào Given. Then phải quan sát được và có giá trị cụ thể (số lượng, phần trăm, nội dung thông báo, trạng thái đúng tên trong spec). Không tự đặt chỉ số hiệu năng (giây, phút, dung lượng): dẫn "theo NFR-xx", hoặc ghi rõ AC chỉ nêu phần chức năng và đưa số vào Câu hỏi mở.
7. Lập ma trận phủ: mỗi mã luồng của spec (kể cả bước con 7a, 7b nếu spec tách) đối chiếu với các AC. Luồng chưa có AC thì ghi "Chưa phủ" kèm lý do.
8. Gắn `[GIẢ ĐỊNH]` cho mọi số, rule, tên không có nguồn. Điều chưa rõ chuyển vào Câu hỏi mở, ghi rõ ai trả lời.

## 4. Mẫu đầu ra
````markdown
## User Story và Acceptance Criteria — <UC-xx tên use case>
Nguồn: <UC-xx, BR-xx, R-xx> · Trạng thái: Nháp chờ BA verify
Quy ước: <ghi các giá trị minh hoạ là [GIẢ ĐỊNH]>

### US-xx · <tên ngắn>
**Là** <vai>, **tôi muốn** <việc>, **để** <giá trị>.
- Truy vết: <UC-xx luồng nào · BR-Cx · R-xx · NFR-xx>
- INVEST: I ✓ · N ✓ · V ✓ · E ✓ · S ✓ · T ✓ (✓ đạt · ⚠ đạt có điều kiện · ✗ không đạt; ⚠ và ✗ phải kèm lý do)

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-01 | Happy | ... | ... | ... | Main 1–8 |
| AC-02 | Lỗi | ... | ... | ... | E1 |
| AC-03 | Biên | ... | ... | ... | A1 |

### Ma trận phủ luồng
| Luồng UC | AC | Ghi chú |
|---|---|---|

### Câu hỏi mở
1. <câu hỏi> — cần <người trả lời>
````

Mã AC đánh liên tục xuyên suốt tài liệu (AC-01, AC-02...), không đánh lại theo từng story. Cột Loại chỉ nhận: Happy, Lỗi, Biên.

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi story đã chấm đủ 6 tiêu chí INVEST (Independent, Negotiable, Valuable, Estimable, Small, Testable), và mọi ⚠ hoặc ✗ đều có lý do?
- [ ] Mỗi AC có đúng một When (hành động đầu vào khác nằm trong Given) và Then kiểm chứng được bằng quan sát, không dùng từ như "nhanh", "thân thiện", "hợp lý"?
- [ ] Mỗi Then có giá trị cụ thể (số lượng, %, nội dung thông báo, đúng tên trạng thái), và AC không tự đặt chỉ số hiệu năng mà dẫn NFR-xx?
- [ ] Mọi exception trong spec đều có AC lỗi, mọi ngưỡng đều có AC dưới, đúng và trên ngưỡng?
- [ ] Cột Luồng UC của từng AC khớp mã luồng thật trong spec, và ma trận phủ không còn luồng bị bỏ sót ngầm?
- [ ] Mọi số, rule, tên không có nguồn đã gắn `[GIẢ ĐỊNH]`, và có mục Câu hỏi mở ở cuối?

## 6. BA phải verify
- Ngưỡng và giới hạn thời gian: AI hay tự đặt số. Xác nhận từng `[GIẢ ĐỊNH]` với stakeholder, nhất là ngưỡng có hai đầu mở (đúng 5% thuộc nhóm nào).
- Cách cắt story: AI có thể cắt quá nhỏ (dư story) hoặc gom quá lớn (vi phạm Small). Đối chiếu với năng lực và nhịp sprint của team.
- AC lẫn yêu cầu phi chức năng hoặc chi tiết giao diện: AI hay chèn số giây, phút vào Then. Hiệu năng thuộc `write-nfr` (AC chỉ dẫn NFR-xx), bố cục thuộc `generate-prototype-screens`. Kiểm số trong AC có lệch NFR không.
- Nhánh lỗi AI đề xuất thêm (không có trong spec) phải được key user công nhận trước khi đưa vào backlog.
- Tính Estimable: story phụ thuộc hệ thống ngoài chưa có tài liệu thì team chưa ước lượng được.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- AC không được chứa số điện thoại, email, giá, công nợ, hợp đồng thật; dùng giá trị bịa và gắn nhãn.
- Không dán nguyên văn email hoặc tin nhắn có thông tin cá nhân vào AC; mô tả bằng vai trò (đại lý, kế toán).

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
