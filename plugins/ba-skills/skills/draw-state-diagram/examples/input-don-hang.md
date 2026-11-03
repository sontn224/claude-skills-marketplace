# Đầu vào mẫu thứ hai: draw-state-diagram (vòng đời Đơn hàng, nối từ UC-01)

Ví dụ này kiểm chuỗi Use Case → State. Dữ kiện từ `_shared/case-dai-viet-electric.md` và spec UC-01 (đầu ra của `write-use-case-spec`). Case hư cấu; mục `[GIẢ ĐỊNH]` là giả định.

## Yêu cầu
Vẽ state diagram và bảng chuyển trạng thái cho entity **Đơn hàng** trong phạm vi UC-01 (F3), có cột "Luồng UC" trích mã bước và luồng của spec.

## Entity
Đơn hàng của đại lý: mã đơn, đại lý, danh sách dòng sản phẩm và số lượng, địa chỉ giao, ngày mong muốn, tổng tiền, chiết khấu, trạng thái.

## Trạng thái cuối luồng nêu trong spec UC-01
- Thành công: "Đã xác nhận" (đơn ghi vào ERP, đại lý nhận email xác nhận).
- A1 xin chiết khấu thêm từ 5% trở lên (tại bước 5) → "Chờ duyệt chiết khấu". Dưới 5%: đại lý tự áp, quay lại bước 5, không đổi trạng thái.
- A2 lưu nháp (tại bước 6) → "Nháp".
- E2 quá hạn công nợ (bước 7, ở 7a) → "Chờ kế toán xử lý".
- E3 ERP không phản hồi (bước 7), E4 mất kết nối khi gửi đơn (bước 6) → "Nháp" `[GIẢ ĐỊNH]`.
- E5 ERP không phản hồi ở bước 2 → use case dừng, chưa có đơn `[GIẢ ĐỊNH]`.
- Sau khi duyệt chiết khấu, đơn tiếp tục từ bước 7a `[GIẢ ĐỊNH]`. Mở lại đơn nháp để tiếp tục từ bước 3 `[GIẢ ĐỊNH]`.

## Business rule liên quan
BR-C1 ngưỡng chiết khấu và người duyệt (`[GIẢ ĐỊNH]` ngưỡng) · BR-C5 lưu người duyệt và thời điểm · BR-C6 đơn chưa duyệt chiết khấu thì chưa ghi vào ERP · BR-C7 quá hạn công nợ thì đơn giữ lại, Kế toán được thông báo.

## Actor và hệ thống có thể kích hoạt
Đại lý · TP Quản lý kênh · Giám đốc Kinh doanh · Kế toán · Hệ thống (kể cả kết quả từ ERP).

## Không có trong đầu vào
Trạng thái sau "Đã xác nhận" (giao hàng, theo dõi đơn thuộc F4) · khi chiết khấu bị từ chối hoặc Kế toán từ chối thì đơn ra sao · ERP lỗi sau khi đã duyệt chiết khấu.
