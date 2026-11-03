# Nhóm chất lượng (ISO/IEC 25010) và cách biến thành NFR

Dùng làm danh mục để không bỏ sót nhóm. Bản 2011 có 8 đặc tính. Bản sửa đổi 2023 đổi tên và bổ sung một số đặc tính (Usability thành Interaction capability, Portability thành Flexibility, thêm Safety). BA nên xác nhận bản đang dùng trong tổ chức; tên nhóm trong output ghi tiếng Việt kèm tên tiếng Anh.

| Nhóm | Phụ đặc tính chính | Câu hỏi làm rõ | Thước đo thường dùng | Cách đo thường gặp |
|---|---|---|---|---|
| Hiệu năng (Performance efficiency) | Time behaviour, resource utilization, capacity | Nhanh với ai, màn hình nào, mạng nào? Bao nhiêu người cùng lúc? | Thời gian phản hồi (phân vị 75 hoặc 95), LCP, dung lượng tải, số người dùng đồng thời, thông lượng | Lighthouse/WebPageTest, load test (JMeter, k6), giám sát hiệu năng |
| Độ tin cậy (Reliability) | Availability, fault tolerance, recoverability, maturity | "Sập" nghĩa là gì? Khi hệ thống ngoài chết thì sao? Mất kết nối giữa chừng thì sao? | Tỷ lệ sẵn sàng (%), thời gian gián đoạn tối đa, RTO/RPO, tỷ lệ lỗi | Giám sát uptime, test ngắt hệ thống ngoài, diễn tập khôi phục |
| Bảo mật (Security) | Confidentiality, integrity, non-repudiation, accountability, authenticity | Ai không được thấy gì? Hành động nào phải truy vết? Mật khẩu theo chính sách nào? | Chính sách mật khẩu, số lần sai tối đa, % hành động có vết, thời gian lưu giữ vết | Kiểm thử cấu hình, test bảo mật, đối chiếu log, rà quyền |
| Khả dụng (Usability / Interaction capability) | Learnability, operability, accessibility, error protection | Người dùng mới làm xong việc chính trong bao lâu, mấy bước? Trên thiết bị nào? | Tỷ lệ hoàn thành tác vụ, thời gian hoàn thành, số bước, điểm SUS | Usability test với người dùng thật, UAT |
| Tương thích (Compatibility) | Co-existence, interoperability | Trình duyệt, thiết bị, hệ thống nào phải chạy cùng? | Danh sách trình duyệt/thiết bị hỗ trợ, tỷ lệ tích hợp thành công | Ma trận kiểm thử, kiểm thử tích hợp |
| Bảo trì (Maintainability) | Modularity, analysability, modifiability, testability | Ai sửa, sửa nhanh cỡ nào, đổi cấu hình có cần dev không? | Thời gian sửa lỗi trung bình, độ bao phủ test, thời gian đổi cấu hình | Số liệu quy trình vận hành, báo cáo kỹ thuật |
| Khả chuyển / Linh hoạt (Portability / Flexibility) | Adaptability, installability, replaceability | Có phải chuyển môi trường hoặc nền tảng không? | Thời gian chuyển, phần dữ liệu và cấu hình mang đi được | Diễn tập chuyển đổi |
| Phù hợp chức năng (Functional suitability) | Completeness, correctness, appropriateness | Phần này đã là yêu cầu chức năng chưa? | Không dùng NFR; chuyển sang user story hoặc use case | Không áp dụng |
| An toàn (Safety, bản 2023) | Hazard warning, fail-safe | Có rủi ro thể chất hoặc tài sản không? | Hiếm gặp ở hệ thống kinh doanh | Phân tích rủi ro |

## Từ mơ hồ và câu hỏi biến chúng thành thước đo
| Từ mơ hồ | Hỏi lại | Hướng thước đo |
|---|---|---|
| Nhanh, mở nhanh | Màn hình/thao tác nào, thiết bị và mạng nào, ai chờ? | Thời gian ở một phân vị, trong điều kiện mạng cụ thể |
| Mạng yếu vẫn dùng được | Yếu là băng thông thấp hay chập chờn? Dùng được nghĩa là xem hay đặt đơn? | Dung lượng tải; không mất dữ liệu khi mất kết nối |
| Không sập, ổn định | Sập là không vào được hay lỗi? Khung giờ nào? | Tỷ lệ sẵn sàng theo khung giờ; tỷ lệ lỗi dưới tải đỉnh |
| Cuối tháng, cao điểm | Bao nhiêu người, bao nhiêu đơn, mấy ngày? | Số người dùng đồng thời, ngày đỉnh |
| Bảo mật, mật khẩu mạnh | Theo chính sách nào, ai kiểm? | Độ dài, thành phần, số lần sai, thời gian khóa |
| Lưu vết | Lưu những gì, bao lâu, ai xem, sửa được không? | % hành động có vết đủ trường; thời gian lưu giữ; số đường sửa vết |
| Dễ dùng | Với ai, làm việc gì, trong bao lâu? | Tỷ lệ hoàn thành, số bước, thời gian |

## Mẫu phát biểu
"Trong điều kiện `<tải/mạng/thiết bị>`, `<hệ thống/chức năng>` phải `<hành vi>`: `<thước đo>` `<≤ hoặc ≥>` `<ngưỡng>`, đo bằng `<cách đo>`."

## Lỗi thường gặp
- Ngưỡng không có điều kiện đo (3 giây ở mạng nào?).
- Trung bình thay vì phân vị: trung bình che những lần rất chậm.
- Nhiều thước đo trong một dòng; tách thành nhiều NFR.
- Cách đo là "kiểm tra" chung chung, không nêu công cụ hay kịch bản.
- Đưa yêu cầu chức năng vào (ví dụ "khóa tài khoản sau 5 lần sai" vừa là chức năng vừa là bảo mật: giữ NFR ở mục tiêu đo được, chi tiết hành vi để user story/AC).
