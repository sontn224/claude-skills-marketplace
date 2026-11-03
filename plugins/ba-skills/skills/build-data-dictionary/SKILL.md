---
name: build-data-dictionary
description: Lập data dictionary, tức bảng định nghĩa từng trường dữ liệu (định nghĩa, định dạng, giá trị hợp lệ, bắt buộc, nguồn), từ ERD hoặc dữ liệu mẫu. Dùng khi đã có thực thể và trường (thường là đầu ra của draft-data-model) và cần chốt chính xác từng trường, ví dụ "lập data dictionary", "định nghĩa các trường", "mô tả field của đơn hàng". Không dùng khi chưa có thực thể và quan hệ (dùng draft-data-model), cần thuật ngữ nghiệp vụ (dùng build-glossary), hay cần phân tích luật nghiệp vụ chi tiết (dùng analyze-business-rules).
---

# Từ điển dữ liệu (Data Dictionary)

## 1. Mục đích
Data Dictionary là bản chuẩn về từng phần tử dữ liệu: nó nghĩa là gì, có định dạng nào, nhận giá trị nào, từ đâu mà có. Nếu ERD cho biết "có gì và nối với gì" thì dictionary cho biết "từng trường chính xác là gì". Mục tiêu là để BA, dev và tester cùng đọc ra một nghĩa, và để mỗi trường có đúng một nguồn sự thật (đặc biệt khi dữ liệu lấy từ hệ thống ngoài như ERP).

## 2. Đầu vào cần có
- ERD (ưu tiên đầu ra của `draft-data-model`) hoặc bảng dữ liệu mẫu đã ẩn danh. Bắt buộc.
- Phạm vi: thực thể nào cần lập dictionary. Bắt buộc; ERD lớn thì hỏi hoặc làm từng thực thể.
- Hệ thống nguồn của từng nhóm trường và quy tắc đã biết (business rule, trạng thái, ngưỡng). Bắt buộc cho cột Nguồn và giá trị hợp lệ.
- Tài liệu kỹ thuật của hệ thống ngoài (ERP). Tùy chọn; không có thì mọi định dạng do ERP quy định gắn `[GIẢ ĐỊNH]`.

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Chốt phạm vi thực thể. Giữ nguyên tên thực thể và trường như trong ERD.
2. Liệt kê trường. Nếu chỉ có dữ liệu mẫu, suy trường từ tên cột và gắn `[GIẢ ĐỊNH]`; không suy giá trị thật thành quy tắc.
3. Viết định nghĩa một câu cho mỗi trường: nó là gì trong nghiệp vụ, không lặp lại tên trường.
4. Ghi định dạng (kiểu, độ dài, mẫu, đơn vị) và giá trị hợp lệ (liệt kê, khoảng, rỗng được hay không).
5. Gán nguồn bằng nhãn cố định: `ERP-đọc`, `Cổng-nhập`, `Cổng-sinh`, `Cổng-tính`, `SSO`. Trường `ERP-đọc` thì ghi rõ không sửa trên hệ thống mới. Mỗi trường đúng một nhãn; trường tham chiếu (khóa ngoại) gắn nhãn theo cách giá trị đi vào trường, phần "mã dùng chung với ERP" để ở Giá trị hợp lệ.
6. Tách trường tính (công thức, không lưu) và quy tắc liên trường (trường A rỗng khi trạng thái B).
7. Đánh dấu trường nhạy cảm; liệt kê giá trị liệt kê kèm căn cứ.
8. Đối chiếu ngược với ERD: không trường thừa, không trường thiếu.

Mẫu đầy đủ (cột mở rộng, ký hiệu định dạng): `references/dictionary-template-full.md`.

## 4. Mẫu đầu ra
````markdown
# Data Dictionary: <thực thể / phạm vi>

## 1. Phạm vi và quy ước
- Phạm vi: <thực thể, nguồn ERD>
- Nhãn nguồn: ERP-đọc · Cổng-nhập · Cổng-sinh · Cổng-tính · SSO
- Quy ước định dạng: <ngày, tiền, mã>

## 2. Bảng trường
### 2.1 <TÊN_THỰC_THỂ>
| Trường | Định nghĩa | Định dạng | Giá trị hợp lệ | Bắt buộc | Nguồn | Nhạy cảm |
|---|---|---|---|---|---|---|

## 3. Giá trị liệt kê
| Trường | Giá trị | Ý nghĩa | Căn cứ |
|---|---|---|---|

## 4. Trường tính và quy tắc liên trường
| Mục | Công thức / quy tắc | Căn cứ |
|---|---|---|

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
````

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mọi trường trong ERD của phạm vi đều có dòng trong bảng (và không có trường lạ)?
- [ ] Mỗi trường có đủ định nghĩa, định dạng, giá trị hợp lệ, bắt buộc và đúng một nhãn nguồn?
- [ ] Trường lấy từ hệ thống ngoài được ghi `ERP-đọc` và không có cột nào cho phép người dùng sửa?
- [ ] Giá trị liệt kê, ngưỡng, độ dài nào không có trong đầu vào đã gắn `[GIẢ ĐỊNH]`?
- [ ] Định nghĩa không vòng tròn (không viết "ngày giao là ngày giao")?
- [ ] Trường tính không bị liệt kê như trường lưu; trường nhạy cảm đã được đánh dấu?

## 6. BA phải verify
- Định dạng của dữ liệu từ hệ thống ngoài (mã ERP, độ dài, mẫu): AI chỉ ví dụ được, không biết thật.
- Giá trị liệt kê đầy đủ: AI hay bỏ sót trạng thái có thật trong vận hành (hủy, giao một phần).
- Ngưỡng và biên (có gồm hay không gồm giá trị biên như đúng 5%).
- Trường bắt buộc "khi nào": bắt buộc lúc lưu nháp hay lúc gửi.
- Đánh dấu nhạy cảm và ai được xem, cần chủ hệ thống hoặc quản trị bảo mật xác nhận.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dữ liệu mẫu phải ẩn danh trước khi dán; ví dụ trong dictionary dùng giá trị bịa.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi định dạng, giá trị, độ dài, ngưỡng không có nguồn trong đầu vào.
- Không suy quy tắc từ vài dòng mẫu: dữ liệu mẫu chỉ gợi ý định dạng, quy tắc phải có nguồn nghiệp vụ.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
