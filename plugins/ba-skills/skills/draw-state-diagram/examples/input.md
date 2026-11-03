# Đầu vào mẫu: draw-state-diagram

Nguồn dữ kiện: `_shared/case-dai-viet-electric.md`, mục Bảo hành (Phase 2). Case hư cấu; mục đánh dấu `[GIẢ ĐỊNH]` là giả định.

## Yêu cầu
Vẽ state diagram và bảng chuyển trạng thái cho entity **Yêu cầu bảo hành** (F6, Phase 2).

## Entity
Yêu cầu bảo hành do đại lý gửi lên cổng. Thuộc tính chính: mã sản phẩm, số serial, ngày mua hoặc mã đơn, mô tả lỗi, ít nhất 2 ảnh (tem serial, vị trí lỗi), địa chỉ và người liên hệ tại công trình, thời điểm gửi.

## Business rule và tình huống
- SLA: phản hồi đầu tiên trong 48 giờ.
- Quá 48 giờ chưa phản hồi: tự động chuyển lên cấp trên `[GIẢ ĐỊNH]`.
- Thời hạn bảo hành 18 tháng từ ngày xuất kho `[GIẢ ĐỊNH]`. Quá hạn bảo hành thì sửa có phí.
- Yêu cầu thiếu ảnh hoặc serial thì phải bổ sung (khoảng 4/10 yêu cầu hiện nay thiếu `[GIẢ ĐỊNH]`).
- Đại lý có thể hủy yêu cầu.

## Actor và hệ thống có thể kích hoạt
Đại lý · Kỹ thuật bảo hành (nhóm của Anh Dũng) · Cấp trên của Kỹ thuật bảo hành · Hệ thống (bộ đếm 48 giờ).

## Không có trong đầu vào
Đại lý được hủy ở trạng thái nào · "phản hồi đầu tiên" gồm những gì · sau khi bổ sung thì SLA tính lại ra sao · "xử lý xong" gồm những bước nào.
