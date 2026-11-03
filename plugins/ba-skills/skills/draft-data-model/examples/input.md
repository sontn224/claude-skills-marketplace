# Đầu vào mẫu: draft-data-model (case Đại Việt Electric)

## Yêu cầu của người dùng
Dựng mô hình dữ liệu logical cho Phase 1 của cổng đại lý, phần báo dự án, đặt hàng và duyệt chiết khấu. Nền tảng cổng chưa chốt nên đừng gắn nền tảng.

## Danh từ nghiệp vụ (rút từ spec)
Đại lý · Dự án đã báo · Đơn hàng · Dòng đơn · Sản phẩm · Phê duyệt chiết khấu

## Spec trích (business rule và use case)
- Đại lý ký hợp đồng theo năm; trả chậm 30–45 ngày tùy hạng `[GIẢ ĐỊNH]`. Sales khu vực phụ trách đại lý (chưa nói một hay nhiều người).
- BR-D1: hai dự án trùng khi giống cả ba: tên dự án, chủ đầu tư, tỉnh/thành.
- BR-D2: mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ.
- BR-D3: bảo hộ 90 ngày kể từ ngày duyệt `[GIẢ ĐỊNH]`.
- BR-D4: báo sau, trùng dự án đang bảo hộ thì thông báo bị trùng.
- BR-D5: đại lý chỉ xem dự án do chính mình báo.
- BR-C1: chiết khấu dưới 5%: đại lý tự áp. Từ 5% đến 10%: TP Quản lý kênh duyệt. Trên 10%: Giám đốc Kinh doanh duyệt `[GIẢ ĐỊNH]`.
- BR-C2: giá niêm yết và tồn kho luôn lấy từ ERP, trên cổng không ai sửa (R6).
- BR-C3: chiết khấu tính trên giá niêm yết, áp cho cả đơn.
- BR-C4: mỗi lần xin chiết khấu phải có lý do.
- BR-C5: quyết định duyệt hoặc từ chối lưu kèm người duyệt và thời điểm (R7).
- BR-C6: đơn chưa duyệt chiết khấu thì chưa ghi vào ERP.
- BR-C7: đại lý quá hạn công nợ thì đơn giữ lại, Kế toán được thông báo (R11).
- BR-P1: phân quyền theo vùng `[GIẢ ĐỊNH]`, chưa có văn bản; liên quan R9 và BR-D5.
- UC-01 Đặt hàng: một đơn gồm nhiều sản phẩm với số lượng; chọn địa chỉ giao và ngày mong muốn; trạng thái Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận; ghi vào ERP thì có mã đơn; đại lý nhận email xác nhận.
- R7: lưu vết mọi thao tác duyệt (ai, lúc nào).
- UC-01 E3 (BA đề xuất `[GIẢ ĐỊNH]`): ERP không phản hồi ở bước 7 (7a hoặc 7b) thì đơn đã gửi quay về Nháp, đại lý được báo thử lại.

## Hệ thống nguồn
- ERP: giá niêm yết, tồn kho, đơn hàng, công nợ. Tài liệu kỹ thuật kết nối ERP chưa có.
- SSO nội bộ: tài khoản nhân viên (không dành cho đại lý).
- Hồ sơ đại lý hiện nằm ở Excel và ERP, đang trùng và thiếu (sẽ import ~300 đại lý theo R8).

## Ràng buộc đã biết
- Nền tảng cổng đại lý chưa chốt (web tùy biến hay Salesforce).
- Bảo hành, báo cáo doanh số thuộc Phase 2, để ngoài.
