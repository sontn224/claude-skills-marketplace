---
name: write-nfr
description: Chuyển mong muốn chất lượng còn mơ hồ ("nhanh", "bảo mật", "không sập") thành yêu cầu phi chức năng đo được, nhóm theo nhóm chất lượng, mỗi yêu cầu có thước đo, ngưỡng và cách đo. Dùng khi stakeholder nói về chất lượng hệ thống mà chưa có con số, ví dụ "viết yêu cầu phi chức năng", "viết NFR", "biến 'chạy nhanh' thành con số". Không dùng khi yêu cầu là hành vi chức năng (dùng write-use-case-spec hoặc write-user-story-and-ac), luật nghiệp vụ (dùng analyze-business-rules) hay soát chất lượng cả tài liệu yêu cầu (dùng pre-review-requirements).
---

# Phân tích yêu cầu phi chức năng (Non-Functional Requirements Analysis)

## 1. Mục đích
Yêu cầu chức năng nói hệ thống làm gì; yêu cầu phi chức năng (NFR) nói hệ thống phải làm tốt đến mức nào và trong điều kiện nào: nhanh, chịu tải, an toàn, dùng được trên mạng yếu. Kỹ thuật này biến những mong muốn chất lượng cảm tính thành phát biểu kiểm chứng được, để dev biết mục tiêu thiết kế, tester biết cách kiểm và sponsor biết mình đang trả tiền cho mức nào. Một NFR chưa có thước đo, ngưỡng và cách đo thì chưa phải là yêu cầu.

## 2. Đầu vào cần có
- Mong muốn chất lượng còn mơ hồ, nguyên văn và nguồn (ai nói, mã yêu cầu như R7, R12). Bắt buộc.
- Bối cảnh sử dụng: ai dùng, thiết bị, mạng, khung giờ cao điểm, số người dùng. Bắt buộc ở mức đã biết; chưa biết thì ghi vào Câu hỏi mở.
- Hệ thống liên quan và ràng buộc (ERP, nền tảng đã chốt chưa). Tùy chọn.
- Số liệu hiện trạng (lưu lượng, sự cố cũ). Tùy chọn; có thì dùng làm căn cứ ngưỡng.

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Tách phần chất lượng khỏi phần chức năng trong mong muốn; ghi nguyên văn kèm nguồn.
2. Gạch các từ mơ hồ ("nhanh", "mạnh", "sập", "yếu") và hỏi: với ai, ở đâu, lúc nào, kém đến mức nào thì tính là hỏng?
3. Gán nhóm chất lượng (danh mục ở `references/iso-25010-groups.md`); một mong muốn có thể thuộc nhiều nhóm.
4. Chọn thước đo cho từng ý (thời gian, tỷ lệ, số lượng) và điều kiện đo (màn hình/luồng, tải, mạng, thiết bị).
5. Đặt ngưỡng. Có số trong đầu vào thì dùng và ghi nguồn; không có thì đề xuất và gắn `[GIẢ ĐỊNH]`, nêu ai cần xác nhận.
6. Nêu cách đo: công cụ hoặc kịch bản, môi trường, ai đo, khi nào (UAT, load test, giám sát).
7. Viết phát biểu theo mẫu "Trong điều kiện X, hệ thống phải Y, đo bằng Z, đạt ngưỡng T".
8. Kiểm lại: mỗi ý trong mong muốn gốc phải sinh ít nhất một NFR (hoặc ghi lý do chưa ra). Rà phụ thuộc và đánh đổi giữa các NFR; NFR chưa đo được vì thiếu dữ liệu thì chuyển vào Câu hỏi mở.

## 4. Mẫu đầu ra
````markdown
# Yêu cầu phi chức năng: <phạm vi>

## 1. Mong muốn gốc và cách hiểu
| Nguồn | Nguyên văn | Từ mơ hồ | Cách hiểu đề xuất |
|---|---|---|---|

## 2. NFR đo được
| ID | Nhóm chất lượng | Nguồn | Yêu cầu | Thước đo | Ngưỡng | Cách đo |
|---|---|---|---|---|---|---|
| NFR-01 | <nhóm> | <R#> | Trong <điều kiện>, <đối tượng> phải <hành vi> | <đại lượng> | <số> `[GIẢ ĐỊNH]` | <công cụ, kịch bản, môi trường> |

## 3. Phụ thuộc và đánh đổi
- <NFR nào phụ thuộc hệ thống/nền tảng nào; NFR nào xung đột nhau>

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
````

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mỗi NFR có đủ thước đo, ngưỡng và cách đo (ba ô đều có số hoặc kịch bản cụ thể)?
- [ ] Không còn từ mơ hồ trong cột Yêu cầu (nhanh, mạnh, ổn định) mà thiếu con số đi kèm?
- [ ] Mọi ngưỡng không có nguồn trong đầu vào đã gắn `[GIẢ ĐỊNH]`; ngưỡng có nguồn ghi rõ nguồn?
- [ ] Điều kiện đo nêu đủ (luồng/màn hình, tải, mạng, thiết bị, môi trường)?
- [ ] Mỗi mong muốn gốc ở mục 1 ra ít nhất một NFR ở mục 2, hoặc có lý do ghi rõ vì sao chưa ra?
- [ ] Không lẫn yêu cầu chức năng vào bảng NFR; xung đột và phụ thuộc đã nêu ở mục 3?

## 6. BA phải verify
- Ngưỡng do AI đề xuất không có căn cứ thực tế: phải được stakeholder và đội kỹ thuật xác nhận bằng dữ liệu hiện trạng.
- NFR có khả thi trên nền tảng và hệ thống ngoài (ERP) hay không; AI không biết giới hạn thật.
- Cách đo có công cụ và môi trường thật để chạy không (ví dụ môi trường test có đủ gần production).
- Điều kiện đỉnh (cuối tháng, chiến dịch): AI suy từ chữ nghĩa, cần số liệu lưu lượng thật.
- Quy định bắt buộc (lưu vết, lưu giữ dữ liệu, chính sách mật khẩu công ty) phải khớp chính sách thật.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Số liệu lưu lượng, sự cố, log dán vào phải đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi ngưỡng, khung giờ, số người dùng, thời gian lưu giữ không có nguồn trong đầu vào.
- Không mô tả chi tiết cấu hình bảo mật nội bộ (tên máy chủ, cách vượt kiểm soát) trong NFR; chỉ nêu mục tiêu và cách kiểm chứng.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
