---
name: write-use-case-spec
description: Viết đặc tả use case đầy đủ 8 phần (main flow, ít nhất 2 alternative flow, ít nhất 3 exception flow) từ yêu cầu và function tree. Dùng khi cần đặc tả cách một actor đạt mục tiêu với hệ thống, ví dụ "viết use case", "đặc tả use case đặt hàng", "viết main flow và exception". Không dùng khi chỉ cần tách và chuẩn hóa business rule (dùng analyze-business-rules), cần user story và acceptance criteria (dùng write-user-story-and-ac), vẽ quy trình nhiều bộ phận (dùng model-business-process), sơ đồ tương tác giữa hệ thống (dùng draw-sequence-diagram) hoặc vòng đời trạng thái (dùng draw-state-diagram).
---

# Đặc tả use case (Use Cases and Scenarios)

## 1. Mục đích
Use Cases and Scenarios mô tả cách một actor tương tác với hệ thống để đạt một mục tiêu có giá trị, gồm luồng thành công và các kịch bản rẽ nhánh hoặc thất bại. BA dùng nó để chốt hành vi hệ thống ở mức đủ rõ cho dev, tester và để làm gốc cho user story, sequence diagram, state diagram. Skill này biến yêu cầu và function tree thành một spec 8 phần có mã bước và mã luồng ổn định để các tài liệu sau trích dẫn.

## 2. Đầu vào cần có
- Yêu cầu liên quan (mã R hoặc đoạn mô tả) và mục tiêu của actor chính.
- Function tree hoặc mã chức năng (F-xx) mà use case thuộc về.
- Danh sách actor và hệ thống ngoài tham gia.
- Tùy chọn: business rule (BR-xx), trạng thái đối tượng, kết quả phỏng vấn, glossary.

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Chốt mục tiêu của actor chính và ranh giới: bắt đầu từ trigger nào, kết thúc khi mục tiêu đạt hay thất bại.
2. Viết Precondition và Postcondition (thành công, thất bại) trước khi viết luồng.
3. Viết main flow: mỗi bước một chủ thể và một hành động, đánh số `1, 2, 3...`. Bước nào gồm hai việc thì tách `7a, 7b` (giữ số gốc 7 để luồng khác còn trích dẫn). Không mô tả giao diện chi tiết.
4. Tìm điểm rẽ nhánh hợp lệ (người dùng chọn khác) và viết alternative flow `A1, A2...`; tối thiểu 2.
5. Tìm điều gì làm luồng không đạt mục tiêu (thiếu hàng, hệ thống ngoài lỗi, mất mạng, quá hạn, không đủ quyền) và viết exception flow `E1, E2, E3...`; tối thiểu 3.
6. Mỗi A/E ghi: điểm rẽ nhánh (tại bước n), các bước xử lý, điểm kết thúc (quay lại bước m hoặc trạng thái cuối). Luồng có hai điểm kết thúc thì ghi cả hai ở tiêu đề, hoặc tách thành hai luồng. Một exception chỉ gắn một bước; lỗi ở bước khác thì tách mã mới.
7. Nếu input có ít hơn 2 A hoặc 3 E: đề xuất thêm và gắn `[GIẢ ĐỊNH]`, nêu lý do ở "Câu hỏi mở".
8. Điền Business rules và truy vết; chỗ rule chưa có mã hoặc nguồn thì gắn `[GIẢ ĐỊNH]`.

Quy tắc mã: mã bước và mã luồng không đổi sau khi đã phát hành. Thêm luồng mới thì đánh mã tiếp theo, không đánh số lại.

## 4. Mẫu đầu ra
Mẫu đầy đủ ở `references/use-case-spec-template.md`. Khung bắt buộc:

````markdown
## UC-xx <Tên use case>
### 1. Thông tin chung
| Mục | Nội dung |
|---|---|
| Mã / Tên | UC-xx / <tên> |
| Mô tả | <một câu: actor đạt được gì> |
| Chức năng liên quan | F-xx |
| Yêu cầu liên quan | R-xx |
| Trigger | <sự kiện bắt đầu> |
### 2. Actor
Chính: <actor> · Phụ / hệ thống ngoài: <danh sách> · Người tham gia ở luồng rẽ nhánh: <nếu có>
### 3. Precondition
- <điều kiện>
### 4. Postcondition
- Thành công: <trạng thái hệ thống sau khi xong>
- Thất bại: <trạng thái khi dừng ở exception>
### 5. Main flow
| Bước | Chủ thể | Hành động |
|---|---|---|
### 6. Alternative flows
**A1 <tên>** (tại bước n) → <kết thúc: quay lại bước m / trạng thái>
1. <bước xử lý>
### 7. Exception flows
**E1 <tên>** (tại bước n) → <kết thúc>
1. <bước xử lý>
### 8. Business rules và truy vết
| Mã | Nội dung | Áp dụng tại | Nguồn |
|---|---|---|---|
### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
````

## 5. Tự kiểm trước khi trả kết quả
- [ ] Đủ 8 phần đúng thứ tự, có ít nhất 2 alternative và 3 exception, mỗi luồng có điểm rẽ nhánh và điểm kết thúc?
- [ ] Mỗi bước main flow có đúng một chủ thể và một hành động (bước gồm hai việc đã tách 7a/7b), không lẫn chi tiết giao diện?
- [ ] Alternative (lựa chọn hợp lệ khác) và exception (không đạt mục tiêu) có bị lẫn vào nhau không?
- [ ] Postcondition thành công và thất bại khớp với điểm kết thúc của các luồng?
- [ ] Mã bước, A, E không trùng, không nhảy số; business rule trích đúng mã (BR-D, BR-C...) của `_shared`; rule chưa có mã thì ghi rõ nguồn?
- [ ] Mọi luồng hoặc rule do AI đề xuất đều có nhãn `[GIẢ ĐỊNH]`?

## 6. BA phải verify
- Exception do AI đề xuất thêm (hệ thống lỗi, mất mạng) có thật sự là rủi ro của dự án và đã bàn với dev chưa.
- Trạng thái đơn ở điểm kết thúc của từng luồng (ví dụ "Nháp", "Chờ kế toán xử lý") có khớp rule nghiệp vụ.
- Ranh giới use case: AI hay nhồi cả duyệt chiết khấu, theo dõi đơn vào một use case; phần của người khác cần tách thành use case riêng.
- Ngưỡng, thời hạn, thông điệp thông báo cho người dùng đều phải được stakeholder xác nhận.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Không đưa thông tin xác thực, token hoặc cấu hình bảo mật thật của hệ thống ngoài vào luồng; chỉ mô tả hành vi.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
