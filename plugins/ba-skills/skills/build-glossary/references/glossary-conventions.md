# Quy ước viết glossary

## Chọn tên chuẩn
1. Ưu tiên từ người dùng nghiệp vụ nói hằng ngày, không phải từ kỹ thuật.
2. Nếu hai từ cùng nghĩa, chọn từ ngắn hơn và ít gây nhầm hơn; từ còn lại vào cột đồng nghĩa.
3. Từ có nhiều nghĩa thì tách thành nhiều thuật ngữ có đối tượng đi kèm (ví dụ "duyệt dự án", "duyệt chiết khấu").
4. Giữ tên vai và tên trạng thái đúng như sẽ hiện trong hệ thống; đổi tên sau sẽ kéo theo sửa use case.

## Viết định nghĩa
- Một đến hai câu, bắt đầu bằng loại sự vật ("Việc ...", "Trạng thái ...", "Người ...").
- Không dùng chính từ đó trong định nghĩa; không dùng từ chưa được định nghĩa.
- Không viết con số hay thời hạn trong định nghĩa nếu chưa có rule xác nhận; để con số ở rule và dẫn mã (BR-*).
- Không mô tả cách hệ thống làm; chỉ nói nghiệp vụ hiểu từ này thế nào.

## Nhãn độ chắc của nguồn
| Nhãn | Khi nào dùng |
|---|---|
| `Có nguồn` | Người có thẩm quyền nói trực tiếp (Fact hoặc Rule trong biên bản), hoặc tài liệu chính thức, không mâu thuẫn |
| `Cần xác minh` | Ý kiến, chỉ một người nói, lời nói mơ hồ, hoặc các nguồn nói khác nhau |
| `[GIẢ ĐỊNH]` | BA hoặc AI suy ra, chưa có nguồn |

## Truy vết sang bước sau
- Danh từ chỉ người hoặc hệ thống → actor trong Use Case.
- Danh từ chỉ trạng thái → state trong sơ đồ trạng thái và trong AC.
- Danh từ chỉ thông tin → trường dữ liệu.
- Động từ có điều kiện → rule (BR-*).
- Mỗi lần đổi tên chuẩn: ghi nhật ký thay đổi và cập nhật nơi dùng.

Nhu cầu (Loại "Nhu cầu" trong biên bản) không dùng làm định nghĩa; chuyển sang rule hoặc yêu cầu.
Trạng thái việc cần làm (`Chưa kiểm chứng`, `Chưa đối chiếu`) giữ riêng, không trộn với nhãn trên.
