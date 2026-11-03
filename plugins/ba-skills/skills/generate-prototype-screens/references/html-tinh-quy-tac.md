# Quy tắc HTML tĩnh (chỉ khi người dùng yêu cầu)

HTML tĩnh chỉ để stakeholder xem thử bố cục và các trạng thái. Không phải code sản phẩm.

## Điều kiện tạo
- Người dùng yêu cầu rõ ràng ("tạo HTML", "cho xem thử trên trình duyệt"). Không có yêu cầu thì không tạo.
- Đã có mô tả màn hình và người dùng đã đồng ý bố cục (hoặc chấp nhận bản nháp).

## Quy tắc
- Một file, không thư viện ngoài, không CSS framework tải từ mạng, không ảnh nhúng từ URL.
- Không JavaScript gọi mạng (không fetch, không form gửi đi). Chuyển trạng thái bằng bộ chọn trạng thái ở đầu trang, hoặc bằng liên kết `#anchor`.
- Chỉ dữ liệu giả. Mỗi giá trị minh hoạ có ghi chú "dữ liệu minh hoạ [GIẢ ĐỊNH]" ở chân trang.
- Có dòng chữ rõ "Bản prototype minh hoạ, chưa phải sản phẩm" ở đầu trang.
- Ngôn ngữ giao diện là tiếng Việt; nhãn và tên trạng thái đúng như mô tả màn hình.
- Bố cục điện thoại: khung rộng tối đa 360 px `[GIẢ ĐỊNH]`, căn giữa.
- Mỗi trạng thái trong mô tả (bình thường, rỗng, lỗi, tải chậm) phải xem được bằng bộ chọn trạng thái.
- Lưu file vào thư mục mà người dùng chỉ định; không tự chọn nơi lưu ngoài dự án.

## Khung tối thiểu
```html
<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>SCR-01 Tạo đơn hàng (prototype)</title>
</head>
<body>
  <p><strong>Bản prototype minh hoạ, chưa phải sản phẩm.</strong></p>
  <nav>Trạng thái:
    <a href="#binh-thuong">Bình thường</a> |
    <a href="#rong">Rỗng</a> |
    <a href="#loi">Lỗi</a> |
    <a href="#tai-cham">Tải chậm</a>
  </nav>
  <section id="binh-thuong"><!-- nội dung màn hình --></section>
  <footer>Dữ liệu minh hoạ [GIẢ ĐỊNH]</footer>
</body>
</html>
```
