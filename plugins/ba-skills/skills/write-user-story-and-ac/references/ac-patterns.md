# Mẫu viết Acceptance Criteria

## Quy tắc Given / When / Then
- Given: trạng thái và dữ liệu ban đầu, đủ để người khác dựng lại. Nêu cả quyền, trạng thái đơn, số liệu, và các thao tác chuẩn bị (đã thêm sản phẩm, đã nhập chiết khấu).
- When: đúng một hành động của actor hoặc một sự kiện (gửi đơn, hết thời gian chờ). Thấy "và", "rồi" trong When thì chuyển phần đầu sang Given.
- Then: kết quả quan sát được. Mỗi Then nên có ít nhất một giá trị cụ thể: con số, đơn vị, hoặc tên trạng thái đúng như spec. Nhiều kết quả thì nối bằng dấu chấm phẩy, mỗi kết quả kiểm được riêng.
- Không nêu tên control hay màu sắc (thuộc `generate-prototype-screens`). Được trích nguyên văn thông báo lỗi nếu đã thống nhất.
- Không tự đặt chỉ số hiệu năng (giây, phút, dung lượng). Dẫn "theo NFR-xx" của `write-nfr`; chưa có NFR thì nêu phần chức năng và đưa chỉ số vào Câu hỏi mở. Thời gian chờ (timeout) cũng là số do NFR hoặc kỹ thuật quy định, AC chỉ viết "hết thời gian chờ".

## Bộ AC tối thiểu cho mỗi story
| Loại | Cần có | Nguồn trong spec |
|---|---|---|
| Happy | 1 AC cho đường chạy thành công | Main flow |
| Lỗi | ít nhất 1 AC cho mỗi exception | E1, E2... |
| Alternative | ít nhất 1 AC cho mỗi luồng rẽ nhánh | A1, A2... |
| Biên | dưới, đúng, trên mỗi ngưỡng; rỗng, 0, tối đa | Business rule, ràng buộc dữ liệu |

## Kỹ thuật nhánh biên
Với ngưỡng T: kiểm giá trị ngay dưới T, đúng T, ngay trên T (và đúng ở đầu kia nếu có khoảng). Trước khi viết, hỏi stakeholder đầu mút có thuộc khoảng không ("từ 5% đến 10%" có gồm đúng 5% và 10% không). Chưa có câu trả lời thì chọn một cách hiểu, gắn `[GIẢ ĐỊNH]`, đưa vào Câu hỏi mở.

Giá trị biên thường gặp: số lượng bằng đúng tồn kho, tồn kho cộng 1, số lượng 0 hoặc để trống, chuỗi rỗng, độ dài tối đa, ngày hôm nay, đúng hạn mức.

## Cách viết lại AC yếu
| AC yếu | Vấn đề | AC tốt hơn |
|---|---|---|
| Hệ thống phản hồi nhanh | Không đo được, và số thuộc NFR | Mã đơn hiện trên màn hình; thời hạn theo NFR-xx |
| Hiện lỗi phù hợp | "Phù hợp" không kiểm được | Hiện "Chỉ còn 20 cuộn trong kho" cạnh dòng sản phẩm |
| Đơn được xử lý đúng | Mơ hồ | Đơn ở trạng thái "Chờ kế toán xử lý" và chưa ghi vào ERP |
| Khi nhập sai thì báo lỗi | Thiếu Given, thiếu giá trị sai cụ thể | Given đơn có tổng 500.000 đ; When nhập chiết khấu âm; Then báo lỗi và tổng đơn không đổi |
| When: thêm 5 cuộn, chọn địa chỉ, rồi gửi đơn | Ba hành động trong một When | Given đã thêm 5 cuộn và chọn địa chỉ; When gửi đơn |

## Ma trận phủ luồng
Mỗi mã luồng của spec phải xuất hiện ít nhất một lần trong cột "Luồng UC". Luồng không có AC thì ghi "Chưa phủ" và lý do (ví dụ chờ quyết định). Nếu AI đề xuất thêm exception ngoài spec, đánh dấu `[GIẢ ĐỊNH]` ở cả mã luồng lẫn AC.
