# Input mẫu — generate-prototype-screens

> Case: Đại Việt Electric (hư cấu). Mọi giá trị đánh dấu `[GIẢ ĐỊNH]` là số bịa để minh hoạ.

## Yêu cầu của người dùng
Dựng mô tả màn hình low-fi cho luồng "Tạo đơn hàng" của đại lý trên điện thoại (R5), gồm trạng thái rỗng, lỗi và tải chậm (R12). Chưa cần HTML tĩnh.

## Thiết bị và actor
Điện thoại, actor chính: Đại lý (ví dụ đại lý Nhân Phát, Đà Nẵng). Nền tảng cổng đại lý (web tùy biến hay Salesforce) chưa chốt.

## Use case spec (tóm lược, UC-01 Đặt hàng)
Main flow: 1 Chọn "Tạo đơn hàng" · 2 Hiển thị danh mục, giá niêm yết, tồn kho từ ERP · 3 Thêm sản phẩm và số lượng · 4 Chọn địa chỉ giao và ngày mong muốn · 5 Tính tổng theo giá niêm yết và chiết khấu chuẩn · 6 Kiểm tra và gửi đơn · 7a Kiểm tra công nợ trên ERP · 7b Ghi đơn vào ERP · 8 Hiển thị mã đơn, gửi email xác nhận.
Alternative: A1 xin chiết khấu thêm (bước 5) → "Chờ duyệt chiết khấu" · A2 lưu nháp (bước 6) → "Nháp".
Exception: E1 không đủ tồn kho (bước 3) · E2 quá hạn công nợ (7a) → "Chờ kế toán xử lý" · E3 ERP không phản hồi ở bước 7 (7a hoặc 7b) → "Nháp" `[GIẢ ĐỊNH]` · E4 mất kết nối khi gửi (bước 6) → "Nháp" `[GIẢ ĐỊNH]` · E5 ERP không phản hồi khi tải danh mục (bước 2) → use case dừng `[GIẢ ĐỊNH]`.
Trạng thái đơn: "Nháp", "Chờ duyệt chiết khấu", "Chờ kế toán xử lý", "Đã xác nhận".
Business rule dùng cho màn hình: BR-C1 (ngưỡng duyệt chiết khấu, `[GIẢ ĐỊNH]`) · BR-C2 (giá và tồn kho từ ERP, không sửa trên cổng) · BR-C3 (chiết khấu tính trên giá niêm yết, áp cả đơn) · BR-C4 (xin chiết khấu phải có lý do) · BR-C7 (quá hạn công nợ thì giữ đơn).

## User story và AC trong phạm vi (đầu ra của write-user-story-and-ac)

| Story | AC | Tóm tắt Then | Luồng UC |
|---|---|---|---|
| US-01 Gửi đơn hàng đủ tồn kho | AC-01 | Tổng đơn 500.000 đ; đơn "Đã xác nhận"; hiện mã đơn; gửi email xác nhận | Main 1–8 |
| | AC-02 | Nhập đúng số lượng bằng tồn kho (20) thì thêm được | Main 3 |
| | AC-03 | Nhập 21 khi tồn 20: hiện "Chỉ còn 20 cuộn trong kho", không gửi được | E1 |
| | AC-04 | Số lượng 0 hoặc trống: hiện "Số lượng tối thiểu là 1" | Main 3 |
| | AC-05 | Quá hạn công nợ: "Chờ kế toán xử lý", đại lý thấy "Đơn đang chờ xử lý", không thấy số công nợ | E2 (7a) |
| US-02 Xin chiết khấu thêm | AC-06 | 4,9%: áp ngay, tổng 475.500 đ | A1 |
| | AC-07, 08 | Đúng 5,0% và đúng 10,0%: "Chờ duyệt chiết khấu", người duyệt là TP Quản lý kênh | A1 |
| | AC-09 | 10,1%: người duyệt là Giám đốc Kinh doanh | A1 |
| | AC-10 | Thiếu lý do (hoặc dưới 10 ký tự): hiện "Nhập lý do xin chiết khấu", không gửi | A1 |
| US-04 Dùng cổng khi mạng yếu hoặc ERP không phản hồi | AC-14 | ERP không phản hồi khi kiểm tra công nợ hoặc ghi đơn: "Chưa gửi được đơn, vui lòng thử lại", đơn về "Nháp" nguyên nội dung (thời hạn theo NFR-06) | E3 (7a/7b) |
| | AC-15 | Gửi lại sau khi ERP đã ghi đơn: kiểm tra ERP trước, không tạo đơn thứ hai | E3 (7b) |
| | AC-16 | Mất kết nối: thông báo lỗi kết nối, đơn "Nháp" nguyên nội dung (NFR-07), gửi lại được | E4 |
| | AC-17 | Gửi lại sau khi đơn đã vào ERP: không tạo đơn thứ hai | E4 |
| | AC-18 | ERP không phản hồi khi tải danh mục: "Chưa tải được danh mục, vui lòng thử lại"; không hiện giá, tồn kho; không tạo đơn nào | E5 (bước 2) |
| | AC-19 | Kết nối chậm: màn hình hiển thị theo NFR-01, có chỉ báo tải, không hiện giá hoặc tồn kho chưa lấy từ ERP | Main 2 (R12) |
| US-05 Lưu nháp | AC-20 | Lưu nháp thành "Nháp", mở lại thấy đủ dòng và địa chỉ | A2 |
| | AC-21 | Đơn chưa có sản phẩm: hiện "Thêm ít nhất 1 sản phẩm", không tạo nháp | A2 |

US-03 (duyệt chiết khấu, AC-11 đến AC-13, thuộc UC-02 chưa viết) là màn hình của TP Quản lý kênh, ngoài phạm vi lần này.

## Dữ liệu minh hoạ `[GIẢ ĐỊNH]`
Sản phẩm SP-0001 "Cáp điện" (nhóm cáp điện), giá niêm yết 100.000 đ/cuộn, tồn 20 cuộn. Mã đơn minh hoạ DH-2026-000101. Địa chỉ giao minh hoạ: "Kho Nhân Phát, Đà Nẵng".
