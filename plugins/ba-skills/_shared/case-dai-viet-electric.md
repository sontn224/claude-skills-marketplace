# Case dùng chung: Đại Việt Electric (hư cấu)

> Nguồn: `40_Knowledge/BA-Training/Case Study Đại Việt Electric.pptx`. Toàn bộ tên riêng và số liệu là giả định.
> Mọi `examples/` phải dùng đúng dữ kiện dưới đây, không bịa thêm tên, mã, số mâu thuẫn với file này. Cần thêm chi tiết thì ghi `[GIẢ ĐỊNH]`.

## Công ty
- Nhà sản xuất thiết bị điện công nghiệp, ~600 nhân viên, nhà máy Bắc Ninh, kho ở ba miền.
- ~200 đại lý, ký hợp đồng theo năm. Ba nhóm sản phẩm: tủ điện, thiết bị đóng cắt, cáp điện.
- Đại lý bán lại cho nhà thầu cơ điện và nhà máy. Sales khu vực phụ trách đại lý; sales admin xử lý đơn.
- Đại lý trả chậm 30–45 ngày tùy hạng `[GIẢ ĐỊNH]`. ~20% đại lý tạo 70% doanh số `[GIẢ ĐỊNH]`.

## Nỗi đau hiện tại
Đặt hàng và báo dự án qua email, Zalo, Excel · sales admin nhập tay vào ERP (~60 đơn/ngày `[GIẢ ĐỊNH]`, sai mã/số lượng) · hai đại lý báo trùng một dự án · duyệt chiết khấu qua Zalo, không lưu vết · không thấy trạng thái đơn · hồ sơ đại lý trùng, thiếu.

## Dự án (5 tháng, 2 phase `[GIẢ ĐỊNH]`)
- Phase 1 (3 tháng): cổng đại lý + CRM nội bộ: đăng ký đại lý, báo dự án, đặt hàng và theo dõi đơn, kết nối ERP, import đại lý cũ (~300).
- Phase 2 (2 tháng): bảo hành, báo cáo doanh số.
- Out of scope: app cho nhà thầu, thanh toán online, sửa ERP, đa ngôn ngữ.
- Quyết định mở: nền tảng cổng đại lý (web tùy biến hay Salesforce). Tài liệu kỹ thuật kết nối ERP chưa có.

## Stakeholder
| Tên | Vai | Đặc điểm |
|---|---|---|
| Anh Quang | Giám đốc Kinh doanh, sponsor | Muốn nhanh, hay thêm yêu cầu; nỗi đau ẩn: không biết sales đang cho chiết khấu bao nhiêu |
| Chị Hạnh | TP Quản lý kênh, key user | Kỹ tính, nói nhanh, kể theo trường hợp; có file Excel riêng theo dõi dự án; bảo vệ đại lý lớn |
| Anh Nhân | Chủ đại lý Nhân Phát (Đà Nẵng) | Ngại thao tác phức tạp, "gọi điện còn nhanh hơn"; sợ lộ mối khách |
| Chị Loan | Kế toán trưởng, chủ ERP | Chậm phản hồi, ngại ảnh hưởng ERP; họp 1 buổi/tuần |
| Anh Dũng | Trưởng Kỹ thuật – Bảo hành | Quá tải, ~15 phút; ~4/10 yêu cầu thiếu ảnh/serial `[GIẢ ĐỊNH]` |
| Anh Kiên | Quản trị hệ thống | Lo phân quyền, bảo mật |

## Actor và hệ thống
Actor: Đại lý · Sales admin · Sales khu vực · TP Quản lý kênh · Giám đốc Kinh doanh · Kế toán · Quản trị hệ thống.
Hệ thống ngoài: ERP (giá niêm yết, tồn kho, đơn hàng, công nợ) · Email · SSO nội bộ (chỉ nhân viên) · Zalo/Excel (hiện trạng).

## Nhu cầu thô R1–R12
- R1 Quang: 70% đơn đại lý qua cổng; thời gian từ nhận đơn đến xác nhận từ 2 ngày xuống 4 giờ `[GIẢ ĐỊNH]`.
- R2 Hạnh: không gõ lại đơn vào ERP.
- R3 Nhân: biết đơn đang ở đâu, bao giờ giao, không phải gọi.
- R4 Hạnh: báo ngay nếu dự án đã có đại lý khác báo.
- R5 Nhân: đặt hàng được trên điện thoại, vài bước.
- R6 Loan: giá và tồn kho lấy từ ERP; không ai sửa giá trên cổng.
- R7 Kiên: mật khẩu mạnh, khóa sau 5 lần sai, lưu vết mọi thao tác duyệt (ai, lúc nào).
- R8 Hạnh: import ~300 đại lý cũ từ Excel và ERP, lọc trùng, đại lý không phải đăng ký lại.
- R9 Quang: sales khu vực xem hết đơn và dự án của mọi đại lý, cả vùng khác. (Mâu thuẫn với BR-D5 phạm vi xem của đại lý và nguyên tắc phân quyền theo vùng; cần làm rõ.)
- R10 Quang: app cho nhà thầu (ngoài scope).
- R11 Loan: đại lý quá hạn công nợ thì không đặt đơn mới, hoặc kế toán được báo trước khi đơn vào ERP.
- R12 Hạnh: cổng mở nhanh, mạng yếu vẫn dùng được, không sập cuối tháng.

## Business rules báo dự án
- BR-D1 Trùng khi giống cả ba: tên dự án, chủ đầu tư, tỉnh/thành.
- BR-D2 Mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ.
- BR-D3 Bảo hộ 90 ngày kể từ ngày duyệt `[GIẢ ĐỊNH]`.
- BR-D4 Báo sau, trùng dự án đang bảo hộ → thông báo bị trùng.
- BR-D5 Đại lý chỉ xem dự án do chính mình báo.

## Business rules đặt hàng và chiết khấu `[GIẢ ĐỊNH]` các ngưỡng
Case gốc không đánh mã cho nhóm rule này. Mã BR-C / BR-P dưới đây do repo ba-skills đặt để truy vết (C = Commerce), không phải mã của case.

| Mã | Rule | Loại |
|---|---|---|
| BR-C1 | Chiết khấu < 5%: đại lý tự áp. 5%–10%: TP Quản lý kênh duyệt. > 10%: Giám đốc Kinh doanh duyệt | Behaviour |
| BR-C2 | Giá niêm yết và tồn kho luôn lấy từ ERP, trên cổng không ai sửa (R6) | Behaviour |
| BR-C3 | Chiết khấu tính trên giá niêm yết, áp cho cả đơn | Definition |
| BR-C4 | Mỗi lần xin chiết khấu phải có lý do | Behaviour |
| BR-C5 | Quyết định duyệt/từ chối lưu kèm người duyệt và thời điểm (R7) | Behaviour |
| BR-C6 | Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP | Behaviour |
| BR-C7 | Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo (R11) | Behaviour |
| BR-P1 | Phân quyền theo vùng `[GIẢ ĐỊNH]`, chưa có văn bản; liên quan R9 và BR-D5 | Behaviour |

Quy ước đầu mút `[GIẢ ĐỊNH]`, chờ trainer xác nhận: đúng 5% và đúng 10% thuộc bậc "5%–10%" (TP Quản lý kênh duyệt); chiết khấu chuẩn của đại lý mặc định 0% khi ví dụ cần một con số.

## UC-01 Đặt hàng
- Actor chính: Đại lý. Hệ thống ngoài: ERP, Email. Precondition: đã đăng nhập, tài khoản hoạt động.
- Postcondition: đơn ghi vào ERP trạng thái "Đã xác nhận"; đại lý nhận email xác nhận.
- Main flow: 1 chọn "Tạo đơn hàng" · 2 hệ thống hiển thị danh mục, giá niêm yết, tồn kho từ ERP · 3 thêm sản phẩm và số lượng · 4 chọn địa chỉ giao và ngày mong muốn · 5 tính tổng theo giá niêm yết và chiết khấu chuẩn · 6 kiểm tra và gửi đơn · 7 hệ thống kiểm tra công nợ trên ERP và ghi đơn · 8 hiển thị mã đơn, gửi email xác nhận.
- Alternative: A1 xin chiết khấu thêm (tại bước 5) → "Chờ duyệt chiết khấu" · A2 lưu nháp (tại bước 6) → "Nháp".
- Exception: E1 không đủ tồn kho (bước 3) · E2 quá hạn công nợ (bước 7) → "Chờ kế toán xử lý".
- Case gốc chỉ có E1, E2. Các exception sau do BA đề xuất, gắn `[GIẢ ĐỊNH]`, và là mã chuẩn cho mọi skill trích dẫn:
  - E3: ERP không phản hồi ở bước 7, tại 7a (kiểm tra công nợ) hoặc 7b (ghi đơn). Đơn về "Nháp", đại lý được báo thử lại; riêng ở 7b, trước khi gửi lại phải kiểm tra đơn đã có trong ERP chưa (tránh tạo đơn trùng). Nếu ERP xử lý 7a và 7b khác nhau thì có thể tách thành hai exception sau.
  - E4: mất kết nối khi đại lý gửi đơn (bước 6). Đơn về "Nháp".
  - E5: ERP không phản hồi khi tải danh mục, giá, tồn kho (bước 2). Use case dừng, chưa có đơn nên không có trạng thái "Nháp".
- Bước 7 gồm hai việc: 7a kiểm tra công nợ trên ERP, 7b ghi đơn vào ERP. Skill nào cần tách thì dùng 7a/7b.

## Bảo hành (Phase 2)
- Đại lý gửi: mã sản phẩm + serial, ngày mua/mã đơn, mô tả lỗi, ≥2 ảnh (tem serial, vị trí lỗi), địa chỉ và người liên hệ tại công trình.
- SLA: phản hồi đầu tiên trong 48 giờ. Thời hạn bảo hành 18 tháng từ ngày xuất kho `[GIẢ ĐỊNH]`.
- Tình huống: thiếu ảnh/serial · quá hạn bảo hành (sửa có phí) · đại lý hủy yêu cầu · quá 48 giờ tự động chuyển lên cấp trên `[GIẢ ĐỊNH]`.

## Tính năng ứng viên F1–F9
F1 Đăng ký đại lý · F2 Báo dự án · F3 Đặt hàng · F4 Theo dõi đơn · F5 Duyệt chiết khấu · F6 Yêu cầu bảo hành · F7 Báo cáo doanh số đại lý · F8 Đa ngôn ngữ · F9 Đăng nhập SSO cho đại lý.

## Change Request giữa chừng
Quang yêu cầu giao diện tiếng Anh (F8) và đăng nhập SSO cho đại lý (F9). Còn 3 sprint × 2 tuần, backlog kín, đa ngôn ngữ đã out of scope, hội nghị đại lý không dời.

## Quy ước mã dùng trong ví dụ
Không dùng dữ liệu thật: số điện thoại, email, giá, công nợ trong ví dụ phải là giá trị bịa và gắn `[GIẢ ĐỊNH]`.

**Mã của case, giữ nguyên:** UC-01 · R1…R12 · F1…F9 · BR-D1…D5 · A1, A2 · E1, E2. Mã repo đặt thêm: BR-C1…C7, BR-P1, E3…E5, US-xx, AC-xx, SCR-xx, NFR-xx.

**Mã có phạm vi theo skill.** Mỗi skill tự đặt tiền tố riêng cho thứ nó sinh ra; trong một tài liệu phải dùng nhất quán. Ba va chạm gây hiểu nhầm nhất đã được đổi thống nhất:

| Loại | Tiền tố chuẩn | Thay cho |
|---|---|---|
| Bước quy trình | P1…Pn | S1…Sn (model-business-process) |
| Gateway / điểm bắt đầu / kết thúc | GW, ST, EN | G1…G8 (gateway) |
| Chỗ thiếu hoặc mâu thuẫn trong tài liệu / rule | GAP-01 | G1…G8 (analyze-source-documents), G-01 (analyze-business-rules) |
| Câu hỏi khảo sát | SQ1…SQn | S1…S11 (design-survey-and-analyze) |
| Câu trả lời khảo sát | TL01… | T01… |
| Chủ đề (khảo sát, retro) | TM1… | C1…C5 (khảo sát), T1…T7 (retro) |
| Cặp thử so khớp | TP1… | T1…T5 (analyze-business-rules) |
| Nguồn tài liệu | S1… | giữ (swot, risks, benchmark) |
| Chuyển trạng thái | T1…Tn | giữ (draw-state-diagram) |
| Câu hỏi phân tích dữ liệu | M0…Mn | Q0…Q4 (mine-usage-data) |

Các mã khác (Q phỏng vấn, QĐ, B/N brainstorm, X xung đột, RT, H, L-, RK-, STR/WEA/OPP/THR, PA-, NFR-, [bN]) giữ nguyên, chỉ có nghĩa trong skill sinh ra chúng.

**Mã ví dụ:** đơn `DH-2026-000101`, sản phẩm `SP-0001`, dòng đơn `DD-…`, đại lý `DL-…`.

**Nhãn độ chắc nguồn, dùng đúng ba giá trị:** `Có nguồn` · `Cần xác minh` · `[GIẢ ĐỊNH]`. Loại phát ngôn (Fact/Rule/Nhu cầu/Ý kiến) chỉ dùng trong biên bản phỏng vấn; khi chuyển sang glossary: Fact hoặc Rule do người có thẩm quyền nói → `Có nguồn`, Ý kiến hoặc một người nói → `Cần xác minh`, Nhu cầu → không dùng làm định nghĩa. Trạng thái việc cần làm (`Chưa kiểm chứng`, `Chưa đối chiếu`, `Chưa phủ`) giữ riêng.

**Thang mức độ:** Cao / Trung bình / Thấp. "Rất cao" chỉ dùng trong thang 5×5 của identify-risks.

**Ký hiệu:** `✓ ⚠ ✗` chỉ dùng cho chấm đạt / có điều kiện / không đạt (INVEST); nơi khác dùng chữ.

**Không đưa nhận xét tính cách stakeholder vào tài liệu chia sẻ** (ví dụ "hay thêm yêu cầu", "chậm phản hồi"); nêu ràng buộc quy trình thay thế. Hồ sơ tính cách chỉ nằm trong phụ lục "chỉ BA".
