# Đầu vào mẫu: write-use-case-spec

Nguồn dữ kiện: `_shared/case-dai-viet-electric.md` (case hư cấu, mọi ngưỡng đánh dấu `[GIẢ ĐỊNH]` là giả định).

## Yêu cầu
Nâng cấp **UC-01 Đặt hàng** lên spec đầy đủ 8 phần, dùng làm gốc cho user story, sequence diagram và state diagram. Cần tối thiểu 2 alternative flow và 3 exception flow.

## Yêu cầu liên quan (rút từ nhu cầu thô)
- R1: 70% đơn đại lý đặt qua cổng; thời gian từ nhận đơn đến xác nhận từ 2 ngày xuống 4 giờ `[GIẢ ĐỊNH]`.
- R2: không gõ lại đơn vào ERP.
- R5: đặt hàng được trên điện thoại, vài bước.
- R6: giá và tồn kho lấy từ ERP; không ai sửa giá trên cổng.
- R7: lưu vết mọi thao tác duyệt (ai, lúc nào).
- R11: đại lý quá hạn công nợ thì không đặt đơn mới, hoặc Kế toán được báo trước khi đơn vào ERP.

## Function tree (Phase 1)
```
Cổng đại lý
├─ F1 Đăng ký đại lý
├─ F2 Báo dự án
├─ F3 Đặt hàng            -> UC-01
│   ├─ Tạo đơn (sản phẩm, số lượng, địa chỉ giao, ngày mong muốn)   [GIẢ ĐỊNH phân rã]
│   ├─ Lưu nháp                                                      [GIẢ ĐỊNH phân rã]
│   ├─ Xin chiết khấu thêm (liên quan F5)                            [GIẢ ĐỊNH phân rã]
│   └─ Gửi đơn (kiểm tra công nợ, ghi ERP, email xác nhận)          [GIẢ ĐỊNH phân rã]
├─ F4 Theo dõi đơn
└─ F5 Duyệt chiết khấu
Phase 2: F6 Yêu cầu bảo hành · F7 Báo cáo doanh số đại lý
Ngoài phạm vi hoặc chưa quyết: F8 Đa ngôn ngữ · F9 Đăng nhập SSO cho đại lý
```

## Dữ kiện UC-01 hiện có
- Actor chính: Đại lý. Hệ thống ngoài: ERP, Email. Precondition: đã đăng nhập, tài khoản hoạt động.
- Postcondition: đơn ghi vào ERP trạng thái "Đã xác nhận"; đại lý nhận email xác nhận.
- Main flow 8 bước: 1 chọn "Tạo đơn hàng" · 2 hiển thị danh mục, giá niêm yết, tồn kho từ ERP · 3 thêm sản phẩm và số lượng · 4 chọn địa chỉ giao và ngày mong muốn · 5 tính tổng theo giá niêm yết và chiết khấu chuẩn · 6 kiểm tra và gửi đơn · 7 kiểm tra công nợ trên ERP và ghi đơn (gồm hai việc: 7a kiểm tra công nợ, 7b ghi đơn) · 8 hiển thị mã đơn, gửi email xác nhận.
- Alternative: A1 xin chiết khấu thêm (bước 5) → "Chờ duyệt chiết khấu" · A2 lưu nháp (bước 6) → "Nháp".
- Exception theo case: E1 không đủ tồn kho (bước 3) · E2 quá hạn công nợ (bước 7) → "Chờ kế toán xử lý". Case chỉ có hai exception; skill yêu cầu tối thiểu 3 nên BA phải đề xuất thêm.

## Business rule đặt hàng và chiết khấu (mã BR-C do repo đặt; ngưỡng `[GIẢ ĐỊNH]`)
- BR-C1: chiết khấu dưới 5% đại lý tự áp; 5%–10% TP Quản lý kênh duyệt; trên 10% Giám đốc Kinh doanh duyệt.
- BR-C2: giá niêm yết và tồn kho luôn lấy từ ERP, trên cổng không ai sửa.
- BR-C3: chiết khấu tính trên giá niêm yết, áp cho cả đơn.
- BR-C4: mỗi lần xin chiết khấu phải có lý do.
- BR-C5: quyết định duyệt hoặc từ chối lưu kèm người duyệt và thời điểm.
- BR-C6: đơn chưa duyệt chiết khấu thì chưa ghi vào ERP.
- BR-C7: đại lý quá hạn công nợ thì đơn giữ lại, Kế toán được thông báo.
