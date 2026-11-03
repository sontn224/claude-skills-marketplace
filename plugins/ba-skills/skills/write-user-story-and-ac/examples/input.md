# Input mẫu — write-user-story-and-ac

> Case: Đại Việt Electric (hư cấu). Mọi giá trị đánh dấu `[GIẢ ĐỊNH]` là số bịa để minh hoạ. Mã BR-C1 đến BR-C7 do repo ba-skills đặt, không phải mã của case gốc.

## Yêu cầu của người dùng
Viết user story và acceptance criteria cho UC-01 Đặt hàng. Cần AC cho happy path, các exception và các ngưỡng chiết khấu (kể cả đúng 5% và đúng 10%).

## Use case spec (đầu ra của write-use-case-spec, bản tóm lược theo 8 phần)

| Phần | Nội dung |
|---|---|
| 1. Thông tin chung | UC-01 Đặt hàng. Chức năng liên quan: F3 Đặt hàng (nhánh xin chiết khấu liên quan F5 Duyệt chiết khấu). Yêu cầu liên quan: R1, R2, R5, R6, R7, R11, R12. Trigger: Đại lý chọn "Tạo đơn hàng" |
| 2. Actor | Chính: Đại lý. Hệ thống ngoài: ERP, Email. Tham gia ở luồng rẽ nhánh: TP Quản lý kênh, Giám đốc Kinh doanh (duyệt chiết khấu), Kế toán (nhận thông báo) |
| 3. Precondition | Đại lý đã đăng nhập, tài khoản hoạt động |
| 4. Postcondition | Thành công: đơn ghi vào ERP trạng thái "Đã xác nhận"; đại lý nhận email xác nhận. Luồng khác: A1 → "Chờ duyệt chiết khấu" · A2 → "Nháp" · E2 → "Chờ kế toán xử lý" · E3, E4 → "Nháp" `[GIẢ ĐỊNH]` · E5 dừng, chưa có đơn nên không có trạng thái `[GIẢ ĐỊNH]` |
| 5. Main flow | 1 Chọn "Tạo đơn hàng". 2 Hiển thị danh mục, giá niêm yết, tồn kho từ ERP. 3 Thêm sản phẩm và số lượng. 4 Chọn địa chỉ giao và ngày mong muốn. 5 Tính tổng theo giá niêm yết và chiết khấu chuẩn. 6 Kiểm tra và gửi đơn. **7a** Kiểm tra công nợ trên ERP. **7b** Ghi đơn vào ERP. 8 Hiển thị mã đơn, gửi email xác nhận |
| 6. Alternative | **A1** Xin chiết khấu thêm (tại bước 5) → đơn "Chờ duyệt chiết khấu"; việc duyệt thuộc F5, use case riêng chưa viết (UC-02), sau khi duyệt đơn tiếp tục từ bước 7a `[GIẢ ĐỊNH]`. **A2** Lưu nháp (tại bước 6) → đơn "Nháp" |
| 7. Exception | **E1** Không đủ tồn kho (bước 3). **E2** Quá hạn công nợ (bước 7a) → "Chờ kế toán xử lý". **E3** ERP không phản hồi ở bước 7 (7a hoặc 7b) → "Nháp"; ở 7b, trước khi gửi lại phải kiểm tra đơn đã có trong ERP chưa `[GIẢ ĐỊNH]`. **E4** Mất kết nối khi gửi đơn (bước 6) → "Nháp", chặn gửi trùng `[GIẢ ĐỊNH]`. **E5** ERP không phản hồi khi tải danh mục, giá, tồn kho (bước 2) → use case dừng `[GIẢ ĐỊNH]` |
| 8. Business rule và truy vết | BR-C1 Chiết khấu < 5% đại lý tự áp; 5%–10% TP Quản lý kênh duyệt; > 10% Giám đốc Kinh doanh duyệt (các ngưỡng `[GIẢ ĐỊNH]`; đúng 5% và đúng 10% thuộc bậc 5%–10% `[GIẢ ĐỊNH]`). BR-C2 Giá niêm yết và tồn kho luôn lấy từ ERP, không ai sửa trên cổng. BR-C3 Chiết khấu tính trên giá niêm yết, áp cả đơn. BR-C4 Mỗi lần xin chiết khấu phải có lý do. BR-C5 Quyết định duyệt hoặc từ chối lưu kèm người duyệt và thời điểm. BR-C6 Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP. BR-C7 Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo |

## NFR liên quan (đầu ra của write-nfr)
NFR-01 màn hình Tạo đơn hàng hiển thị nội dung chính (LCP) · NFR-03 phản hồi mở danh mục có giá và tồn kho từ ERP · NFR-06 khi ERP không phản hồi, cổng vẫn mở được, lưu được đơn Nháp và có thông báo rõ · NFR-07 mất kết nối lúc gửi đơn không làm mất dữ liệu đơn đang nhập. Ngưỡng cụ thể nằm ở write-nfr, không chép lại vào AC.

## Dữ liệu minh hoạ `[GIẢ ĐỊNH]`
Sản phẩm SP-0001 (nhóm cáp điện): giá niêm yết 100.000 đ/cuộn, tồn kho 20 cuộn. Đơn minh hoạ: 5 cuộn, tổng niêm yết 500.000 đ; chiết khấu chuẩn 0%.
