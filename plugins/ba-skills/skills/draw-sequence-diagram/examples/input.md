# Đầu vào mẫu: draw-sequence-diagram

Nguồn dữ kiện: `_shared/case-dai-viet-electric.md` và spec UC-01 (đầu ra của `write-use-case-spec`). Case hư cấu; mục đánh dấu `[GIẢ ĐỊNH]` là giả định.

## Yêu cầu
Vẽ sequence diagram cho **UC-01 Đặt hàng**: main flow và các exception có tương tác với ERP hoặc Email (E1, E2, E3). Không cần vẽ A1, A2, E4, E5.

## Hệ thống và actor liên quan
- Đại lý (actor chính) · Cổng đại lý (hệ thống đang xây; spec gọi là "Hệ thống") · ERP (ngoài: giá niêm yết, tồn kho, đơn hàng, công nợ) · Email (ngoài) · Kế toán (nhận thông báo ở E2).

## Spec UC-01 (rút gọn, giữ nguyên mã)
Precondition: đại lý đã đăng nhập, tài khoản hoạt động.

Main flow:
1. Đại lý chọn "Tạo đơn hàng".
2. Hệ thống hiển thị danh mục, giá niêm yết, tồn kho lấy từ ERP.
3. Đại lý thêm sản phẩm và số lượng.
4. Đại lý chọn địa chỉ giao và ngày mong muốn.
5. Hệ thống tính tổng theo giá niêm yết và chiết khấu chuẩn.
6. Đại lý kiểm tra đơn và gửi đơn.
7a. Hệ thống kiểm tra công nợ của đại lý trên ERP.
7b. Hệ thống ghi đơn vào ERP.
8. Hệ thống hiển thị mã đơn và gửi email xác nhận cho đại lý.

Exception (E1, E2 theo case; E3, E4, E5 do BA đề xuất `[GIẢ ĐỊNH]`):
- E1 Không đủ tồn kho (bước 3): hệ thống không nhận số lượng vượt tồn, hiển thị tồn kho hiện có; đại lý chỉnh lại, quay về bước 3.
- E2 Quá hạn công nợ (bước 7, ở 7a): hệ thống không ghi đơn vào ERP, giữ đơn ở "Chờ kế toán xử lý" (giữ tại cổng `[GIẢ ĐỊNH]`), thông báo Kế toán qua Email `[GIẢ ĐỊNH]`, báo đại lý đơn chưa xác nhận.
- E3 ERP không phản hồi khi ghi đơn (bước 7, ở 7a hoặc 7b) `[GIẢ ĐỊNH]`: đơn về "Nháp" và báo đại lý thử lại; trước khi gửi lại ở 7b phải kiểm tra đơn đã có trong ERP chưa.
- E4 Mất kết nối khi đại lý gửi đơn (bước 6) `[GIẢ ĐỊNH]`: đơn về "Nháp". Không vẽ.
- E5 ERP không phản hồi khi tải danh mục, giá, tồn kho (bước 2) `[GIẢ ĐỊNH]`: use case dừng, chưa có đơn nên không có "Nháp". Không vẽ.

## Thông tin tích hợp
Chưa có tài liệu kỹ thuật kết nối ERP (đồng bộ hay bất đồng bộ, thời gian chờ chưa biết). Chị Loan (chủ ERP) chưa phản hồi.
