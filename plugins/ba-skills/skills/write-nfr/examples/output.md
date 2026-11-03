# Yêu cầu phi chức năng: Cổng đại lý Đại Việt Electric, Phase 1 (từ R12 và R7)

## 1. Mong muốn gốc và cách hiểu
| Nguồn | Nguyên văn | Từ mơ hồ | Cách hiểu đề xuất |
|---|---|---|---|
| R12 (Chị Hạnh) | "mở nhanh" | nhanh | Màn hình chính của đại lý (tạo đơn) hiện nội dung chính trong vài giây trên điện thoại ở mạng 4G chậm; đo ở một phân vị, không phải trung bình |
| R12 (Chị Hạnh) | "mạng yếu vẫn dùng được" | yếu, dùng được | Băng thông thấp (giả lập Slow 4G `[GIẢ ĐỊNH]`) và kết nối chập chờn: trang nhẹ, và đơn đang nhập không mất khi mất kết nối |
| R12 (Chị Hạnh) | "không sập cuối tháng" | sập, cuối tháng | Sập là không truy cập được hoặc lỗi quá ngưỡng; cuối tháng là 3 ngày cuối tháng có tải đỉnh `[GIẢ ĐỊNH]`; cũng không sập theo khi ERP chậm hoặc không phản hồi |
| R7 (Anh Kiên) | "mật khẩu mạnh" | mạnh | Chính sách độ dài và thành phần cụ thể, kiểm được bằng mẫu mật khẩu yếu |
| R7 (Anh Kiên) | "khóa sau 5 lần sai" | (đã có số 5) | Số lần sai là 5 (từ nguồn); còn thiếu thời gian khóa và cách mở khóa |
| R7 (Anh Kiên) | "lưu vết mọi thao tác duyệt (ai, lúc nào)" | mọi, lưu vết | Mọi quyết định duyệt hoặc từ chối dự án và chiết khấu đều có bản ghi đủ trường, không sửa được, lưu đủ lâu |

## 2. NFR đo được
Mọi ngưỡng có nhãn `[GIẢ ĐỊNH]` là con số đề xuất, chưa có nguồn từ khách hàng, cần xác nhận trước khi chốt.

| ID | Nhóm chất lượng | Nguồn | Yêu cầu | Thước đo | Ngưỡng | Cách đo |
|---|---|---|---|---|---|---|
| NFR-01 | Hiệu năng (Performance efficiency): thời gian đáp ứng | R12 | Trong điều kiện điện thoại tầm trung giả lập và mạng Slow 4G, màn hình Tạo đơn hàng phải hiển thị nội dung chính | LCP (Largest Contentful Paint), trung vị của 5 lần chạy | ≤ 3,0 giây `[GIẢ ĐỊNH]` | Lighthouse hoặc WebPageTest, profile mobile Slow 4G, chạy trên môi trường staging trước mỗi release |
| NFR-02 | Hiệu năng (Performance efficiency): dung lượng | R12 | Trong lần tải đầu (cache trống), màn hình Tạo đơn hàng không được truyền quá dung lượng cho phép | Tổng byte truyền đã nén của lần tải đầu | ≤ 1,5 MB `[GIẢ ĐỊNH]` | Chrome DevTools tab Network hoặc Lighthouse "total byte weight", cache trống |
| NFR-03 | Hiệu năng (Performance efficiency): thời gian đáp ứng | R12, BR-C2 | Trong giờ thường (tối đa 30 người dùng đồng thời `[GIẢ ĐỊNH]`), mở danh mục sản phẩm kèm giá niêm yết và tồn kho từ ERP phải phản hồi | Thời gian phản hồi đầu-cuối, phân vị 95 | ≤ 2,0 giây `[GIẢ ĐỊNH]` | Kịch bản load test UC-01 bước 2 trên staging có ERP test; ghi riêng thời gian phía ERP |
| NFR-04 | Hiệu năng (Performance efficiency): sức chứa | R12 | Trong 3 ngày cuối tháng, cổng phải chịu tải đỉnh mà không sập | Số người dùng đồng thời giữ được với phân vị 95 ≤ 3 giây và tỷ lệ lỗi dưới 1% | ≥ 100 người dùng đồng thời `[GIẢ ĐỊNH]` (khoảng 200 đại lý, giả định 50% cùng online) | Load test (JMeter hoặc k6) kịch bản UC-01, tăng tải từ 100% đến 150% để tìm giới hạn, chạy trước go-live |
| NFR-05 | Độ tin cậy (Reliability): sẵn sàng | R12 | Trong giờ làm việc 07:00 đến 19:00, thứ Hai đến thứ Bảy `[GIẢ ĐỊNH]`, cổng phải truy cập được | Availability = phút truy cập được ÷ tổng phút giờ làm việc, tính theo tháng; thời gian gián đoạn liên tục dài nhất trong 3 ngày cuối tháng | ≥ 99,5% `[GIẢ ĐỊNH]`; gián đoạn liên tục ≤ 5 phút `[GIẢ ĐỊNH]` | Giám sát uptime, ping giả lập mỗi 1 phút từ ít nhất 2 vị trí; báo cáo hằng tháng |
| NFR-06 | Độ tin cậy (Reliability): chịu lỗi | R12, BR-C2 | Khi ERP không phản hồi, cổng vẫn mở được các chức năng không phụ thuộc ERP và hiển thị thông báo rõ: ở bước 2 (E5) use case dừng; ở bước 7b (E3) đơn về Nháp | Tỷ lệ chức năng không phụ thuộc ERP vẫn dùng được; thời gian chờ ERP tối đa; thời gian từ lúc hết chờ đến lúc có thông báo | 100% vẫn dùng được; chờ ERP tối đa 30 giây `[GIẢ ĐỊNH]`; thông báo trong ≤ 10 giây sau khi hết chờ `[GIẢ ĐỊNH]` | Test mô phỏng ERP timeout trên staging ở hai điểm: tải danh mục (E5, bước 2) và ghi đơn (E3, bước 7b); E3, E5 do BA đề xuất `[GIẢ ĐỊNH]` |
| NFR-07 | Độ tin cậy (Reliability): khôi phục | R12 | Khi mất kết nối lúc gửi đơn (E4, bước 6), dữ liệu đơn đang nhập không bị mất và đơn về Nháp | Số đơn mất dữ liệu ÷ số lần thử ngắt mạng | 0 trên 20 lần thử `[GIẢ ĐỊNH]` | Test thủ công trên điện thoại: ngắt mạng ở UC-01 bước 6 (E4, BA đề xuất `[GIẢ ĐỊNH]`), bật lại, kiểm tra đơn còn nguyên ở Nháp hoặc đã gửi đúng một lần |
| NFR-08 | Bảo mật (Security): xác thực | R7 | Hệ thống phải từ chối mật khẩu yếu khi đặt hoặc đổi mật khẩu | Độ dài và thành phần tối thiểu; số mẫu mật khẩu yếu bị từ chối | ≥ 10 ký tự, có chữ hoa, chữ thường và số `[GIẢ ĐỊNH]`; 10 trên 10 mẫu yếu bị từ chối | Kiểm tra cấu hình chính sách và bộ 10 mẫu mật khẩu yếu; Anh Kiên đối chiếu chính sách công ty |
| NFR-09 | Bảo mật (Security): chống dò mật khẩu | R7 | Sau 5 lần nhập sai liên tiếp, tài khoản bị khóa | Số lần sai kích hoạt khóa; thời gian khóa | 5 lần (nguồn R7); khóa 15 phút hoặc đến khi quản trị mở khóa `[GIẢ ĐỊNH]` | Test: nhập sai 5 lần, lần 6 nhập đúng vẫn bị từ chối; kiểm tra bản ghi khóa |
| NFR-10 | Bảo mật (Security): truy vết | R7, BR-C5 | Mọi quyết định duyệt hoặc từ chối dự án và chiết khấu phải được ghi vết | Tỷ lệ quyết định có bản ghi vết đủ trường: người duyệt, thời điểm, kết quả, đối tượng được duyệt | 100% (R7 nói "mọi"); trường kết quả và đối tượng là phần thêm `[GIẢ ĐỊNH]` | Trên staging thực hiện 30 quyết định duyệt `[GIẢ ĐỊNH cỡ mẫu]` rồi đối chiếu với bản ghi vết, số lệch bằng 0 |
| NFR-11 | Bảo mật (Security): toàn vẹn và lưu giữ vết | R7, BR-C5 | Bản ghi vết không được sửa hoặc xóa qua giao diện, và được lưu đủ lâu | Số đường sửa hoặc xóa bản ghi vết qua giao diện của mọi vai; thời gian lưu giữ | 0 đường; ≥ 36 tháng `[GIẢ ĐỊNH]` | Rà quyền với mọi vai kể cả Quản trị hệ thống; kiểm tra cấu hình lưu giữ |

## 3. Phụ thuộc và đánh đổi
- NFR-01 đến NFR-05 phụ thuộc nền tảng cổng chưa chốt (web tùy biến hay Salesforce). Ngưỡng chỉ chốt được sau khi có nền tảng và kiểm giới hạn của nó.
- NFR-03 và NFR-06 phụ thuộc ERP (BR-C2). Cổng không cam kết nhanh hơn ERP trả lời; cần tách thời gian phía ERP khỏi thời gian phía cổng khi đo. Chưa có tài liệu kỹ thuật ERP; trao đổi với chủ ERP theo lịch họp một buổi mỗi tuần.
- NFR-09 và trải nghiệm: khóa sau 5 lần sai có thể khiến đại lý ở xa (đại lý cần thao tác ít bước, R5) phải gọi hỗ trợ; cần cách mở khóa đơn giản.
- NFR-10 và NFR-03: ghi vết đồng bộ làm chậm thao tác duyệt; cần thống nhất vết ghi cùng giao dịch hay ghi bất đồng bộ nhưng không được mất bản ghi.
- NFR-04 và NFR-05 tăng chi phí hạ tầng; mức sẵn sàng 99,5% là lựa chọn cần sponsor chấp thuận.
- Chưa đề cập nhóm Tương thích (thiết bị, trình duyệt), phiên hết hạn, mã hóa đường truyền: R7 và R12 chưa nhắc nên chưa đưa vào bảng.

### Câu hỏi mở
1. "Mạng yếu" thực tế của đại lý là gì (3G, 4G chập chờn, vùng nào), có đo thử ở Đà Nẵng được không? Dùng để chốt NFR-01, NFR-02, NFR-07. (Anh Nhân, Chị Hạnh)
2. Cuối tháng có bao nhiêu đại lý và bao nhiêu đơn cùng lúc, ngày đỉnh là ngày nào? Lấy từ email, Excel, ERP hiện tại để thay cho con số 100 người dùng đồng thời. (Chị Hạnh, Chị Loan)
3. Chính sách mật khẩu và thời gian khóa của công ty là gì, mở khóa do ai và bằng cách nào? (Anh Kiên)
4. "Mọi thao tác duyệt" có gồm cả việc Kế toán xử lý đơn quá hạn công nợ không? Thời gian lưu vết theo quy định nội bộ hoặc pháp lý là bao lâu? (Anh Kiên, Chị Loan)
5. ERP có độ trễ, giới hạn gọi đồng thời hoặc cửa sổ bảo trì nào cần tính vào NFR-03, NFR-06? Cần tài liệu kỹ thuật kết nối. (Chị Loan)
6. Mức sẵn sàng và chi phí hạ tầng cho NFR-04, NFR-05 có chấp nhận được không, hay giảm ngưỡng? (Anh Quang)
7. E3 (ERP không phản hồi khi ghi đơn), E4 (mất kết nối khi gửi) và E5 (ERP không phản hồi khi tải danh mục) là exception BA đề xuất `[GIẢ ĐỊNH]`; NFR-06, NFR-07 chỉ có kịch bản kiểm khi key user công nhận và đưa vào Phase 1. Thời gian chờ ERP 30 giây có chấp nhận được không? (Chị Hạnh, Chị Loan)
8. Có cần thêm NFR cho thiết bị, trình duyệt hỗ trợ, thời gian phiên và mã hóa đường truyền không? (Anh Kiên, Anh Quang)
