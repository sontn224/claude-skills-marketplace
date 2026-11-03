# Input mẫu: analyze-business-rules

Dữ liệu hư cấu của case Đại Việt Electric. Mọi tên riêng và số liệu là giả định.

## Yêu cầu của BA
Phân tích các rule báo dự án và rule đặt hàng/chiết khấu của Phase 1: phân loại, và tìm chỗ mâu thuẫn hoặc chưa rõ. Có hai băn khoăn cụ thể:
1. Đại lý A báo một dự án, đã được duyệt và đang bảo hộ. Sau đó đại lý B báo lại cùng dự án nhưng gõ khác chữ hoa/thường, hoặc gõ khác một ký tự. BR-D1 có coi là trùng không?
2. R9 có va với BR-D5 không?

Dữ liệu thử cho băn khoăn 1 (giả định; mã cặp thử TP1…TP5):
- Dự án gốc (đại lý A, đã duyệt): tên "Nhà xưởng KCN Alpha - GĐ2", chủ đầu tư "Công ty TNHH Beta", tỉnh/thành "Bắc Ninh".
- Cặp TP1: đại lý B báo tên "NHÀ XƯỞNG KCN ALPHA - GĐ2" (chỉ khác hoa/thường), các thuộc tính còn lại giống hệt.
- Cặp TP2: tên "Nhà xưởng KCN Alpha - GĐ 2" (thừa một khoảng trắng).
- Cặp TP3: tên "Nhà xưởng KCN Alpha - GD2" (gõ Đ thành D, khác một ký tự).
- Cặp TP4: tên "Nhà xưởng KCN Alpha - GĐ3" (khác một ký tự nhưng có thể là một dự án khác thật).
- Cặp TP5: chủ đầu tư viết "Cty TNHH Beta", các thuộc tính còn lại giống hệt.

## Business rules báo dự án
- BR-D1 Trùng khi giống cả ba: tên dự án, chủ đầu tư, tỉnh/thành.
- BR-D2 Mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ.
- BR-D3 Bảo hộ 90 ngày kể từ ngày duyệt `[GIẢ ĐỊNH]`.
- BR-D4 Báo sau, trùng dự án đang bảo hộ thì thông báo bị trùng.
- BR-D5 Đại lý chỉ xem dự án do chính mình báo.

## Rule đặt hàng và chiết khấu (mã BR-C do repo đặt, ngưỡng là `[GIẢ ĐỊNH]`)
- BR-C1 Chiết khấu < 5%: đại lý tự áp. 5%–10%: TP Quản lý kênh duyệt. > 10%: Giám đốc Kinh doanh duyệt.
- BR-C2 Giá niêm yết và tồn kho luôn lấy từ ERP, trên cổng không ai sửa (R6).
- BR-C3 Chiết khấu tính trên giá niêm yết, áp cho cả đơn.
- BR-C4 Mỗi lần xin chiết khấu phải có lý do.
- BR-C5 Quyết định duyệt/từ chối lưu kèm người duyệt và thời điểm (R7).
- BR-C6 Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP.
- BR-C7 Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo (R11).
- BR-P1 Phân quyền theo vùng `[GIẢ ĐỊNH]`, chưa có văn bản; liên quan R9 và BR-D5.

Quy ước đầu mút `[GIẢ ĐỊNH]`, chờ trainer xác nhận: đúng 5% và đúng 10% thuộc bậc "5%–10%" (TP Quản lý kênh duyệt); chiết khấu chuẩn của đại lý mặc định 0% khi ví dụ cần một con số.

## Yêu cầu liên quan
- R4 (Chị Hạnh): Báo ngay nếu dự án đã có đại lý khác báo.
- R9 (Anh Quang): Sales khu vực xem hết đơn và dự án của mọi đại lý, cả vùng khác.
- R11 (Chị Loan): Đại lý quá hạn công nợ thì không đặt đơn mới, hoặc kế toán được báo trước khi đơn vào ERP.

## Ngữ cảnh khác
- Sales khu vực phụ trách đại lý.
- Đại lý trả chậm 30–45 ngày tùy hạng `[GIẢ ĐỊNH]`.
- UC-01 Đặt hàng: bước 5 tính tổng theo giá niêm yết và chiết khấu chuẩn; bước 7 hệ thống kiểm tra công nợ trên ERP rồi ghi đơn. Alternative A1: xin chiết khấu thêm (tại bước 5) → trạng thái "Chờ duyệt chiết khấu". Exception E2: quá hạn công nợ (bước 7) → "Chờ kế toán xử lý".
