# Đầu vào mẫu: write-nfr (case Đại Việt Electric)

## Yêu cầu của người dùng
Chuyển hai mong muốn R12 và R7 thành yêu cầu phi chức năng đo được cho cổng đại lý Phase 1. Mọi con số ngưỡng tự đề xuất phải gắn `[GIẢ ĐỊNH]` và nêu cách đo.

## Mong muốn gốc (nguyên văn rút gọn từ nhu cầu thô)
- R12 (Chị Hạnh, TP Quản lý kênh): cổng mở nhanh, mạng yếu vẫn dùng được, không sập cuối tháng.
- R7 (Anh Kiên, Quản trị hệ thống): mật khẩu mạnh, khóa sau 5 lần sai, lưu vết mọi thao tác duyệt (ai, lúc nào).

## Bối cảnh sử dụng đã biết
- Khoảng 200 đại lý; mục tiêu 70% đơn đại lý đi qua cổng (R1). Hiện khoảng 60 đơn mỗi ngày `[GIẢ ĐỊNH]`.
- Đại lý đặt hàng trên điện thoại (R5), có đại lý ở xa như Đà Nẵng; đại lý cần thao tác ít bước (R5).
- Giá niêm yết và tồn kho lấy từ ERP (BR-C2, R6). Tài liệu kỹ thuật kết nối ERP chưa có; chủ ERP là Chị Loan, họp một buổi mỗi tuần.
- Nền tảng cổng đại lý chưa chốt (web tùy biến hay Salesforce).
- Thao tác duyệt trong phạm vi: duyệt dự án (BR-D2, TP Quản lý kênh) và duyệt chiết khấu (BR-C1, TP Quản lý kênh hoặc Giám đốc Kinh doanh); quyết định phải lưu kèm người duyệt và thời điểm (BR-C5).
- UC-01 Đặt hàng: bước 2 hiển thị danh mục, giá, tồn kho từ ERP; bước 6 gửi đơn; bước 7 gồm 7a kiểm tra công nợ trên ERP và 7b ghi đơn vào ERP. Exception theo case: E1 không đủ tồn kho, E2 quá hạn công nợ. BA đề xuất thêm `[GIẢ ĐỊNH]`: E3 ERP không phản hồi ở bước 7 (7a hoặc 7b) → đơn về Nháp; E4 mất kết nối khi gửi đơn (bước 6) → đơn về Nháp; E5 ERP không phản hồi khi tải danh mục, giá, tồn kho (bước 2) → use case dừng, chưa có đơn.

## Chưa có
- Số liệu lưu lượng thực tế cuối tháng, định nghĩa "mạng yếu", chính sách mật khẩu công ty, thời gian lưu vết theo quy định.
