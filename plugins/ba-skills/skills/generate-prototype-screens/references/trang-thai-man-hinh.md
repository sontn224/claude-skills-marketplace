# Danh mục trạng thái màn hình

Mỗi màn hình mô tả đủ các trạng thái dưới đây. Trạng thái không áp dụng thì ghi "không áp dụng" kèm lý do một dòng.

| Trạng thái | Khi nào xuất hiện | Cần mô tả | Nguồn trong spec |
|---|---|---|---|
| Bình thường | Có dữ liệu, mọi thứ hoạt động | Bố cục đầy đủ, hành động chính | Main flow |
| Rỗng | Chưa có dữ liệu (giỏ trống, kết quả tìm không có) | Câu giải thích, hành động tiếp theo | Điều kiện trước hoặc AC dạng biên rỗng |
| Lỗi nhập liệu | Người dùng nhập sai | Vị trí lỗi (gắn vào trường), nội dung cụ thể, hành động sửa | Exception, AC lỗi |
| Lỗi hệ thống | Hệ thống ngoài không phản hồi | Thông báo, cách thử lại, dữ liệu người dùng được giữ | Exception hạ tầng |
| Tải chậm | Đang lấy dữ liệu | Chỉ báo đang tải (khung chờ), phần nào dùng được, phần nào khoá | Yêu cầu hiệu năng hoặc AC "tải chậm" |
| Mất mạng | Thiết bị mất kết nối (điện thoại) | Banner, dữ liệu giữ lại, cách gửi lại | Exception mất mạng |
| Đang gửi | Sau khi bấm gửi, chờ phản hồi | Khoá nút gửi để tránh gửi hai lần | AC chống trùng |
| Không đủ quyền | Actor không có quyền hành động | Ẩn hay vô hiệu hoá, có giải thích không | Business rule phân quyền |
| Thành công | Hoàn tất | Kết quả, mã tham chiếu, bước tiếp theo | Postcondition |

## Quy tắc viết nội dung
- Thông báo lỗi nêu đúng con số, tên trường, và việc cần làm. Ví dụ "Chỉ còn 20 cuộn trong kho" thay vì "Số lượng không hợp lệ".
- Trạng thái rỗng luôn kèm một hành động tiếp theo (nút hoặc gợi ý).
- Trạng thái tải chậm không hiển thị dữ liệu chưa lấy xong (giá, tồn kho). Dùng khung chờ.
- Nút hành động chính đặt cố định ở cuối màn hình điện thoại để dễ chạm bằng một tay.
- Vùng chạm tối thiểu khoảng 44 px `[GIẢ ĐỊNH]` (quy ước phổ biến, cần team design xác nhận).

## Quy ước wireframe text
- Khung bằng ký tự đơn giản; nút viết `[ Nhãn ]`; ô nhập `[__________]`; danh sách chọn `[ Nhãn v ]`; liên kết `<Nhãn>`.
- Điện thoại: một cột, rộng khoảng 30 ký tự. Máy tính: tối đa hai cột.
- Chỉ một wireframe cho mỗi màn hình; các trạng thái còn lại mô tả bằng bảng, chỉ vẽ lại phần thay đổi.
