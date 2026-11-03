---
name: mine-usage-data
description: Lập kế hoạch khai thác dữ liệu sử dụng đã ẩn danh sau go-live gồm câu hỏi phân tích, truy vấn SQL, gợi ý biểu đồ và các bước đối chiếu số trước khi kết luận. Dùng khi BA có dữ liệu ẩn danh (đơn hàng, log sử dụng) và cần đo giải pháp so với mục tiêu, ví dụ "khai thác dữ liệu sử dụng", "viết SQL đo chỉ số đơn hàng so với mục tiêu", "đối chiếu số trước khi kết luận". Không dùng khi đã biết chỉ số xấu và cần hỏi vì sao (dùng analyze-root-cause), khi cần mô tả cấu trúc bảng và cột (dùng build-data-dictionary), khi cần ý kiến người dùng (dùng design-survey-and-analyze), hoặc khi dữ liệu chưa ẩn danh (phải ẩn danh trước, ngoài phạm vi skill này).
---

# Khai thác dữ liệu (Data Mining)

## 1. Mục đích
Data Mining là việc đi qua một khối dữ liệu có sẵn để tìm mẫu hình, xu hướng và bất thường giúp trả lời một câu hỏi nghiệp vụ. Ở giai đoạn Solution Evaluation, skill này giúp BA biến mục tiêu đã cam kết (ví dụ R1) thành câu hỏi đo được, truy vấn chạy được, và quy trình kiểm số để kết luận không dựa vào con số chưa kiểm. Skill chỉ mô tả "dữ liệu cho thấy gì", không giải thích "vì sao".

## 2. Đầu vào cần có
- Dữ liệu **đã ẩn danh** (bảng hoặc mẫu vài chục dòng) kèm tên cột, kiểu dữ liệu, ý nghĩa từng cột.
- Mục tiêu hoặc ngưỡng cần so sánh (ví dụ R1: 70% đơn qua cổng, xác nhận trong 4 giờ).
- Giai đoạn dữ liệu, múi giờ, nguồn trích xuất (cổng, ERP hay bản gộp) và cách ẩn danh.
- Tùy chọn: hệ quản trị CSDL (mặc định PostgreSQL), nguồn đối chiếu sẵn có (ERP, báo cáo kế toán).

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa cột, số dòng hay kết quả.

## 3. Các bước
1. Chốt chỉ số từ mục tiêu: tử số, mẫu số, đơn vị, mốc thời gian bắt đầu và kết thúc. Mục tiêu mơ hồ (trung bình hay % trong ngưỡng?) thì ghi vào câu hỏi mở.
2. Đọc lược đồ dữ liệu, ghi giới hạn: cỡ mẫu, cột thiếu, giai đoạn, múi giờ.
3. Viết câu hỏi phân tích: mỗi câu một chỉ số, gắn với một mục tiêu. Câu "vì sao" chuyển sang analyze-root-cause.
4. Đặt truy vấn kiểm chất lượng dữ liệu (M0). Tách **dòng lỗi** (trùng khóa, null bất thường, giờ ngược thứ tự) khỏi **dòng hợp lệ nhưng ngoài mẫu số** (bản nháp, hủy). Nêu dòng nào bị loại, loại khỏi chỉ số nào, và lý do.
5. Viết SQL cho từng câu hỏi: dùng CTE, đặt tên cột rõ, ghi điều kiện lọc và dialect. Xem `references/sql-va-bieu-do.md`.
6. Tự tính tay kết quả mẫu trên chính dữ liệu input; không có input thì để trống kết quả, không bịa.
7. Gợi ý biểu đồ theo loại câu hỏi (so sánh, phân phối, xu hướng) và nêu cảnh báo đọc biểu đồ.
8. Lập bảng đối chiếu: số nào, đối chiếu với nguồn nào, ai sở hữu nguồn, tiêu chí khớp. Số chưa đối chiếu chỉ được gọi là "sơ bộ".
9. Viết nhận định sơ bộ bằng "dữ liệu cho thấy", không dùng "do", "nhờ", "vì". Đề xuất skill tiếp theo nếu cần tìm nguyên nhân.

## 4. Mẫu đầu ra
```
## Kế hoạch khai thác dữ liệu: <chủ đề>
### A. Phạm vi và dữ liệu
(nguồn, giai đoạn, múi giờ, số dòng, cột, cách ẩn danh, giới hạn)
### B. Câu hỏi phân tích
| ID | Câu hỏi | Gắn với | Chỉ số và định nghĩa | Ngưỡng đối chiếu |
### C. Truy vấn SQL
(mỗi ID một khối ```sql, dòng đầu ghi dialect và định nghĩa lọc)
### D. Kết quả mẫu từ dữ liệu input
(mỗi ID một bảng; số tính lại được từ input)
### E. Gợi ý biểu đồ
| ID | Loại biểu đồ | Trục và đường tham chiếu | Cảnh báo |
### F. Đối chiếu số trước khi kết luận
| # | Số cần đối chiếu | Giá trị trong dữ liệu | Nguồn đối chiếu | Người sở hữu | Tiêu chí khớp | Trạng thái |
### G. Nhận định sơ bộ
(mô tả, kèm ghi chú "chưa kết luận" nếu F chưa khớp)
### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
```

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi câu hỏi có chỉ số, định nghĩa tử số và mẫu số, ngưỡng đối chiếu (hoặc ghi rõ chưa có ngưỡng)?
- [ ] Mỗi truy vấn chạy đúng logic trên bảng input, và mọi số ở mục D tính lại khớp?
- [ ] Có M0 kiểm chất lượng dữ liệu và nêu rõ dòng bị loại cùng lý do?
- [ ] Mọi con số trong nhận định đều có trong mục D; không con số nào suy ra ngoài dữ liệu?
- [ ] Bảng đối chiếu nêu nguồn, người sở hữu, trạng thái, và nhận định ghi rõ "chưa kết luận" khi chưa khớp?
- [ ] Nhận định tránh từ chỉ nhân quả và có cảnh báo cỡ mẫu nhỏ?

## 6. BA phải verify
- AI hay bịa số hoặc làm tròn cho đẹp: BA chạy lại SQL trên dữ liệu ẩn danh thật và đối chiếu với ERP.
- AI hay nhầm tương quan với nhân quả (ví dụ "cổng làm đơn nhanh hơn" trong khi nhóm đơn và nhóm đại lý có thể khác nhau). Phần "vì sao" phải qua kiểm chứng.
- Định nghĩa chỉ số do AI tự hiểu: "thời gian xác nhận" tính từ giờ nhận đơn hay giờ nhập? Mục tiêu 4 giờ là trung bình, trung vị hay % đơn? BA chốt với sponsor.
- Cú pháp SQL theo dialect và múi giờ thật của hệ thống; AI không thấy lược đồ thật. SQL trong ví dụ mới được tính lại bằng script, chưa chạy trên PostgreSQL thật: BA tự chạy trên môi trường được phép rồi so với kết quả mẫu.
- Mẫu nhỏ và ngoại lệ có thể kéo trung bình; luôn xem thêm trung vị và số dòng.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Chỉ dùng dữ liệu đã ẩn danh hoặc mã hóa một chiều; không để bảng ánh xạ mã sang tên cạnh dữ liệu.
- Không dán cột giá, công nợ, hợp đồng, tên, số điện thoại, email. Bỏ các cột đó trước khi đưa vào.
- Nhóm quá nhỏ (dưới 5 dòng) có thể nhận diện đại lý: gộp nhóm hoặc không báo cáo riêng.
- AI không chạy truy vấn trên hệ thống thật; BA tự chạy trong môi trường được phép.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
