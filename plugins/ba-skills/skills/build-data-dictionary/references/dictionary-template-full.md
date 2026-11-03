# Mẫu data dictionary đầy đủ

Dùng khi cần chi tiết hơn bảng 7 cột trong SKILL.md (ví dụ bàn giao cho dev, hoặc dictionary sẽ thành nguồn cho test).

## Các cột mở rộng (thêm khi cần)
| Cột | Nội dung | Khi nào thêm |
|---|---|---|
| Tên hiển thị | Nhãn trên giao diện, tiếng Việt có dấu | Khi đã có prototype |
| Mặc định | Giá trị khi tạo mới | Khi có rule mặc định |
| Ai được sửa | Vai trò được ghi/sửa trường | Khi phân quyền theo trường |
| Khi nào khóa | Từ trạng thái nào trường không sửa được | Trường như tỷ lệ chiết khấu, đơn giá |
| Quy tắc kiểm tra | Điều kiện validate và thông báo lỗi | Khi chuyển cho dev/test |
| Ví dụ hợp lệ / không hợp lệ | Hai ví dụ bịa, không phải dữ liệu thật | Trường có định dạng dễ nhầm |
| Lưu giữ | Thời gian giữ, có xóa được không | Trường lịch sử, vết duyệt |
| Căn cứ | Mã BR, UC, R liên quan | Luôn nên có |

## Ký hiệu định dạng nên dùng
| Loại | Cách ghi | Ví dụ bịa |
|---|---|---|
| Mã | Tiền tố + phân đoạn, nêu số ký tự | `DH-` + năm 4 số + `-` + 6 số |
| Ngày | ISO 8601 khi lưu, `DD/MM/YYYY` khi hiển thị | lưu `2026-11-20`, hiển thị `20/11/2026` |
| Ngày giờ | ISO 8601 kèm múi giờ | `2026-11-03T09:30:00+07:00` |
| Tiền | Số, đơn vị tiền, số chữ số thập phân, làm tròn | VND, không thập phân |
| Phần trăm | Số, bao nhiêu chữ số thập phân, có phải là phần trăm hay hệ số | `7,50` nghĩa là 7,5% |
| Chuỗi | Độ dài tối đa, ký tự cho phép | tối đa 255 ký tự |
| Liệt kê | Liên kết sang mục "Giá trị liệt kê" | `trang_thai` |
| Tham chiếu | Trỏ khóa của thực thể nào | `DAI_LY.ma_dai_ly` |

## Nhãn nguồn
| Nhãn | Nghĩa | Ai sửa được |
|---|---|---|
| ERP-đọc | Hệ thống ERP là nguồn sự thật; hệ thống mới chỉ đọc hoặc chụp lại | Không ai trên hệ thống mới |
| Cổng-nhập | Người dùng nhập trên hệ thống mới | Vai trò nêu ở cột "Ai được sửa" |
| Cổng-sinh | Hệ thống tự sinh hoặc tự đổi (mã, thời điểm, trạng thái theo sự kiện) | Không ai |
| Cổng-tính | Tính từ trường khác; không lưu | Không ai |
| SSO | Đồng bộ từ danh tính nội bộ | Quản trị danh tính |

## Định nghĩa tốt và dở
| Dở | Tốt | Vì sao |
|---|---|---|
| "Ngày giao" | "Ngày đại lý muốn nhận hàng, đại lý chọn khi tạo đơn" | Phân biệt mong muốn và dự kiến |
| "Trạng thái đơn" | "Vị trí của đơn trong quy trình xử lý, đổi theo sự kiện hệ thống" | Nói ai đổi và theo gì |
| "Giá" | "Giá niêm yết của một đơn vị tại thời điểm thêm dòng, lấy từ ERP" | Nêu thời điểm và nguồn |

## Câu hỏi làm rõ trường hay thiếu
1. Rỗng được không, và rỗng trong trạng thái nào?
2. Sửa được sau khi gửi không? Ai sửa?
3. Có ngưỡng biên không, biên có gồm giá trị đó không?
4. Giá trị này đã có ở hệ thống khác chưa; nếu có, ai là nguồn sự thật?
5. Trường này có lộ thông tin cá nhân hoặc thương mại không?
