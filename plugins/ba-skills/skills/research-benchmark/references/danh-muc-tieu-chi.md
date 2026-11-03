# Danh mục tiêu chí benchmark (gợi ý)

Dùng khi người dùng chưa có tiêu chí. Đây là gợi ý để người dùng chọn; AI không tự chốt tiêu chí và không điền nội dung từ danh mục này vào bảng so sánh.

## Nhóm tiêu chí cho so sánh nền tảng hoặc giải pháp phần mềm
| Nhóm | Câu hỏi gợi ý | Bằng chứng chấp nhận được |
|---|---|---|
| Phù hợp chức năng | Đáp ứng bao nhiêu tính năng trong phạm vi hiện tại, phần nào phải tự xây? | Tài liệu sản phẩm, bản demo có ghi chú, ánh xạ yêu cầu với tính năng |
| Tích hợp | Kết nối với hệ thống hiện có bằng cách nào, ai làm, cần tài liệu gì? | Tài liệu kỹ thuật của cả hai phía, xác nhận của chủ hệ thống |
| Bảo mật và phân quyền | Phân quyền theo vai trò, theo vùng, lưu vết thao tác có sẵn hay phải tự làm? | Tài liệu bảo mật, xác nhận của quản trị hệ thống |
| Trải nghiệm người dùng | Dùng được trên điện thoại, mạng yếu, số bước thao tác chính? | Bản demo thử có người dùng thật, ghi chú quan sát |
| Chi phí | Chi phí ban đầu, chi phí định kỳ, mô hình tính phí, chi phí ẩn? | Báo giá chính thức, ước lượng của đội triển khai |
| Thời gian và năng lực | Có kịp mốc không, đội hiện có làm được không, cần tuyển hay thuê? | Ước lượng effort của đội, kế hoạch dự án |
| Mở rộng | Đáp ứng giai đoạn sau và thay đổi yêu cầu (đa ngôn ngữ, đăng nhập một lần) thế nào? | Tài liệu sản phẩm, lộ trình do nhà cung cấp xác nhận |
| Vận hành và hỗ trợ | Ai bảo trì, SLA hỗ trợ, nâng cấp, phụ thuộc nhà cung cấp? | Hợp đồng hỗ trợ, điều khoản dịch vụ |
| Rủi ro nhà cung cấp | Mức khóa chặt (lock-in), tính ổn định, khả năng thoát? | Điều khoản hợp đồng, tham chiếu khách hàng |

## Nhóm tiêu chí cho phân tích thị trường và đối thủ
| Nhóm | Câu hỏi gợi ý | Bằng chứng chấp nhận được |
|---|---|---|
| Nhu cầu và phân khúc | Ai là khách hàng, nhu cầu chính, phân khúc nào ưu tiên? | Khảo sát, dữ liệu bán hàng nội bộ ẩn danh, báo cáo ngành do người dùng cung cấp |
| Đối thủ | Ai cạnh tranh trực tiếp, khác biệt chính ở đâu? | Tài liệu công khai của đối thủ do người dùng đưa |
| Xu hướng | Thay đổi nào của công nghệ, quy định, hành vi khách hàng ảnh hưởng? | Báo cáo có nguồn |
| Quy mô thị trường | Quy mô, tăng trưởng (chỉ khi có số liệu từ nguồn) | Báo cáo có nguồn; không có thì để `Cần xác minh` |

## Thang độ tin cậy của nguồn
| Mức | Loại nguồn | Cách dùng |
|---|---|---|
| Cao | Tài liệu chính thức, báo giá, hợp đồng, xác nhận bằng văn bản của chủ hệ thống | Được điền thẳng vào ô, ghi ID nguồn |
| Trung bình | Bản demo có ghi chú, báo cáo bên thứ ba có tên rõ | Điền kèm ghi chú độ tin cậy |
| Thấp | Ghi chú cá nhân, "nghe nói", kinh nghiệm chưa kiểm chứng | Chỉ ghi vào ô kèm nhãn `Cần xác minh` |
| Không có | AI nhớ hoặc suy đoán | Không điền. Ghi `Cần xác minh`, hoặc `[GIẢ ĐỊNH]` kèm cơ sở nếu là suy luận logic |

## Cách ghi ô khi thiếu nguồn
- Không có thông tin: `Cần xác minh` + việc cần làm (ví dụ "xin báo giá").
- Suy luận từ định nghĩa, không phải từ sản phẩm cụ thể: `[GIẢ ĐỊNH]: <cơ sở>`.
- Không dùng cụm "thường", "nhìn chung", "theo thị trường" thay cho nguồn.
