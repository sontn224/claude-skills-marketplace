# Đầu vào mẫu: model-business-process

Nguồn dữ kiện: `_shared/case-dai-viet-electric.md` (case hư cấu, mọi ngưỡng đánh dấu `[GIẢ ĐỊNH]` là giả định).

## Yêu cầu
Vẽ quy trình **To-be** đặt hàng của đại lý trên cổng đại lý (Phase 1, F3 Đặt hàng và F5 Duyệt chiết khấu). Dùng làm nền cho UC-01.

## Mô tả quy trình bằng chữ (ghi chú của BA sau buổi làm việc)
- Đại lý đăng nhập, chọn "Tạo đơn hàng". Cổng hiển thị danh mục, giá niêm yết và tồn kho lấy từ ERP (không ai sửa giá trên cổng).
- Đại lý thêm sản phẩm và số lượng, chọn địa chỉ giao và ngày mong muốn. Nếu số lượng vượt tồn kho thì phải chỉnh lại.
- Cổng tính tổng theo giá niêm yết và chiết khấu chuẩn.
- Đại lý có thể xin chiết khấu thêm, kèm lý do. Chiết khấu dưới 5% đại lý tự áp; từ 5% đến 10% TP Quản lý kênh duyệt; trên 10% Giám đốc Kinh doanh duyệt `[GIẢ ĐỊNH]` các ngưỡng. Mỗi quyết định lưu người duyệt và thời điểm.
- Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP.
- Khi gửi đơn, cổng kiểm tra công nợ của đại lý trên ERP. Nếu đại lý quá hạn công nợ, đơn bị giữ lại ở "Chờ kế toán xử lý" và Kế toán được thông báo. Nếu không, đơn được ghi vào ERP với trạng thái "Đã xác nhận" và đại lý nhận email xác nhận.
- Đại lý cũng có thể lưu nháp thay vì gửi ngay.

## Actor và hệ thống
Đại lý · TP Quản lý kênh · Giám đốc Kinh doanh · Kế toán · Cổng đại lý · ERP · Email (gửi qua cổng).

## Sự kiện bắt đầu và kết quả
Bắt đầu: Đại lý cần đặt hàng. Kết thúc: đơn "Đã xác nhận" trong ERP, hoặc đơn ở "Nháp", hoặc đơn không được chấp nhận.

## Không có trong ghi chú (BA chưa hỏi)
Khi chiết khấu bị từ chối thì đơn đi đâu · Kế toán xử lý đơn bị giữ như thế nào · thời hạn duyệt · ERP không phản hồi thì sao.
