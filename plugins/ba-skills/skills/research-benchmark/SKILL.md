---
name: research-benchmark
description: Lập bảng so sánh có nguồn giữa các đối tượng (phương án, sản phẩm, đối thủ, thực hành) theo tiêu chí do người dùng đưa, ô nào chưa có nguồn thì ghi rõ cần xác minh. Dùng khi cần cơ sở chọn giữa các phương án hoặc xem vị thế so với thị trường, ví dụ "so sánh phương án", "benchmark nền tảng", "phân tích thị trường đối thủ". Không dùng khi cần tổng quan điểm mạnh/yếu của một tổ chức (dùng draft-swot), liệt kê rủi ro của phương án đã chọn (dùng identify-risks) hoặc chỉ đọc một tài liệu có sẵn để tóm tắt, rút yêu cầu, rule, thuật ngữ (dùng analyze-source-documents).
---

# Benchmarking và phân tích thị trường (Benchmarking and Market Analysis)

## 1. Mục đích
Benchmarking so sánh một đối tượng với các đối tượng khác (đối thủ, phương án thay thế, thực hành tốt) qua cùng một bộ tiêu chí, để thấy khoảng cách và chọn hướng. Market Analysis nhìn rộng hơn: nhu cầu, phân khúc, đối thủ, xu hướng. Skill này chỉ dựng bảng so sánh từ nguồn người dùng đưa. Nó **không tự tra hay tự nhớ** giá, tính năng, số liệu thị trường: AI rất dễ bịa những thứ này.

## 2. Đầu vào cần có
- Mục đích quyết định: so sánh để chọn gì, ai quyết (bắt buộc).
- Danh sách đối tượng so sánh, tối thiểu hai (bắt buộc).
- Tiêu chí so sánh do người dùng đưa, kèm mức quan trọng nếu có (bắt buộc). Chưa có thì gợi ý từ `references/danh-muc-tieu-chi.md` để người dùng chọn, không tự chốt.
- Tài liệu nguồn về từng đối tượng: tài liệu sản phẩm, báo giá, báo cáo thị trường, ghi chú demo, ghi chú của người dùng (bắt buộc ít nhất một nguồn; thiếu thì vẫn dựng bảng nhưng ô trống là "Cần xác minh").
- Ràng buộc và yêu cầu của dự án để đặt ngưỡng cho tiêu chí (tùy chọn).

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Nhắc lại mục đích quyết định và danh sách đối tượng; xác nhận phạm vi.
2. Lập bảng nguồn: gán ID S1, S2..., ghi loại nguồn (tài liệu chính thức, báo giá, ghi chú cá nhân, yêu cầu dự án) và độ tin cậy.
3. Lập bảng tiêu chí: mỗi tiêu chí có nguồn gốc (do người dùng đưa hoặc từ yêu cầu nào), mức quan trọng, ngưỡng cần đạt nếu có.
4. Điền từng ô (tiêu chí x đối tượng) chỉ bằng nội dung có trong nguồn, kèm ID nguồn. Ghi chú cá nhân không có tài liệu đi kèm vẫn được ghi nhưng đánh `Cần xác minh`.
5. Ô không có nguồn: ghi `Cần xác minh`. Ô AI suy ra từ logic (không phải từ nguồn): ghi `[GIẢ ĐỊNH]` và nêu cơ sở suy luận. Không điền số, giá, tên tính năng từ trí nhớ.
6. Nhận xét: chỉ nêu khác biệt có nguồn; nói rõ phần nào chưa đủ cơ sở để kết luận. Không xếp hạng bằng điểm khi phần lớn ô chưa có nguồn.
7. Đánh giá mức sẵn sàng ra quyết định; lập danh sách việc cần xác minh (ô nào, cần gì, từ ai).
8. Nêu câu hỏi mở.

## 4. Mẫu đầu ra
```
## Benchmark: <chủ đề>
Mục đích quyết định: <...> | Đối tượng: <A>, <B> | Ngày: <...>

### 1. Nguồn đã dùng
| ID | Tài liệu | Loại nguồn | Độ tin cậy |

### 2. Tiêu chí
| ID | Tiêu chí | Nguồn tiêu chí | Mức quan trọng | Ngưỡng / yêu cầu |

### 3. Bảng so sánh
| Tiêu chí | <Đối tượng A> | <Đối tượng B> |
Mỗi ô: <nội dung> - <Sx> hoặc "Cần xác minh" hoặc "[GIẢ ĐỊNH]: <cơ sở>"

### 4. Nhận xét
- Khác biệt đã có nguồn: ...
- Chưa đủ cơ sở: ...

### 5. Mức sẵn sàng ra quyết định và việc cần xác minh
Kết luận: Đủ / Chưa đủ cơ sở để khuyến nghị
| Ô (tiêu chí x đối tượng) | Cần gì | Từ ai / nguồn nào |

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
```
Ví dụ đầy đủ: `examples/output.md`.

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mọi ô trong bảng so sánh có một trong ba thứ: ID nguồn có thật trong bảng nguồn, `Cần xác minh`, hoặc `[GIẢ ĐỊNH]` kèm cơ sở?
- [ ] Không có giá, số liệu thị trường, tên hay tính năng sản phẩm nào xuất hiện mà không có trong nguồn người dùng đưa?
- [ ] Cột tiêu chí đúng bộ tiêu chí người dùng đưa, không tự thêm hay bỏ; thêm gợi ý thì tách riêng và nói rõ?
- [ ] Các đối tượng được điền cùng mức chi tiết (không thiên vị một bên vì có nhiều nguồn hơn mà không ghi chú)?
- [ ] Mục 5 nêu thẳng mức sẵn sàng ra quyết định và từng việc xác minh có người hoặc nguồn cụ thể?
- [ ] Đầu ra kết thúc bằng "Câu hỏi mở", câu hỏi xuất phát từ chỗ thiếu thật của nguồn?

## 6. BA phải verify
- Giá, tính năng, giới hạn kỹ thuật của sản phẩm thật: AI dễ bịa hoặc dùng thông tin cũ. Mọi ô quyết định phải đối chiếu tài liệu chính thức hoặc báo giá.
- Số liệu thị trường (quy mô, thị phần, tăng trưởng): AI dễ bịa số trông hợp lý. Chỉ chấp nhận số có nguồn gốc người dùng cung cấp.
- Ghi chú cá nhân hoặc "nghe nói" đã được giữ nhãn `Cần xác minh`, chưa bị nâng thành sự thật.
- Tiêu chí và trọng số phản ánh đúng ưu tiên của người quyết định, không phải của AI.
- Ràng buộc đang mơ hồ trong yêu cầu (chưa chốt, mâu thuẫn) ảnh hưởng đến mọi phương án: kiểm tra đã được nêu ở nhận xét chưa.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Không đưa thông tin mật của đối thủ hoặc khách hàng (báo giá riêng, hợp đồng, tài liệu có NDA) vào đầu ra nếu chưa được phép; chỉ dùng thông tin công khai hoặc đã được cho phép chia sẻ.
- Báo giá của nhà cung cấp là thông tin nhạy cảm: ghi nguồn bằng ID, không dán nguyên văn vào tài liệu lưu hành rộng.

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
