## UC-01 Đặt hàng
### 1. Thông tin chung
| Mục | Nội dung |
|---|---|
| Mã / Tên | UC-01 / Đặt hàng |
| Mô tả | Đại lý tạo và gửi đơn hàng trên cổng; đơn được ghi vào ERP và đại lý nhận xác nhận mà không phải gõ lại |
| Chức năng liên quan | F3 Đặt hàng (nhánh xin chiết khấu liên quan F5 Duyệt chiết khấu) |
| Yêu cầu liên quan | R1, R2, R5, R6, R7, R11 |
| Trigger | Đại lý chọn "Tạo đơn hàng" |

### 2. Actor
Chính: Đại lý · Phụ / hệ thống ngoài: ERP, Email · Người tham gia ở luồng rẽ nhánh: TP Quản lý kênh, Giám đốc Kinh doanh (duyệt chiết khấu, A1), Kế toán (nhận thông báo, E2)

### 3. Precondition
- Đại lý đã đăng nhập, tài khoản hoạt động.

### 4. Postcondition
- Thành công: đơn được ghi vào ERP với trạng thái "Đã xác nhận"; đại lý nhận email xác nhận.
- Thất bại hoặc dừng ở luồng khác: A1 (từ 5%) → "Chờ duyệt chiết khấu" · A2 → "Nháp" · E1 giữ đơn đang soạn · E2 → "Chờ kế toán xử lý" · E3, E4 → "Nháp" `[GIẢ ĐỊNH]` · E5 → use case dừng, chưa có đơn nên không có trạng thái "Nháp" `[GIẢ ĐỊNH]`. Trong mọi trường hợp này, đơn chưa ghi vào ERP.

### 5. Main flow
| Bước | Chủ thể | Hành động |
|---|---|---|
| 1 | Đại lý | Chọn "Tạo đơn hàng" |
| 2 | Hệ thống | Hiển thị danh mục, giá niêm yết, tồn kho lấy từ ERP |
| 3 | Đại lý | Thêm sản phẩm và số lượng |
| 4 | Đại lý | Chọn địa chỉ giao và ngày mong muốn |
| 5 | Hệ thống | Tính tổng theo giá niêm yết và chiết khấu chuẩn |
| 6 | Đại lý | Kiểm tra đơn và gửi đơn |
| 7a | Hệ thống | Kiểm tra công nợ của đại lý trên ERP |
| 7b | Hệ thống | Ghi đơn vào ERP |
| 8 | Hệ thống | Hiển thị mã đơn và gửi email xác nhận cho đại lý |

Bước 7 của case gồm hai việc nên tách thành 7a và 7b; các luồng bên dưới vẫn nói "bước 7".

### 6. Alternative flows
**A1 Xin chiết khấu thêm** (tại bước 5) → hai điểm kết thúc tùy mức: (a) dưới 5%: quay lại bước 5 · (b) từ 5% trở lên: kết thúc với đơn "Chờ duyệt chiết khấu"
1. Đại lý chọn "Xin chiết khấu thêm", nhập tỷ lệ và lý do (bắt buộc).
2. Hệ thống xác định mức: dưới 5% đại lý tự áp, hệ thống tính lại tổng rồi quay lại bước 5 (kết thúc (a)); từ 5% đến 10% người duyệt là TP Quản lý kênh; trên 10% là Giám đốc Kinh doanh `[GIẢ ĐỊNH]` các ngưỡng và đầu mút.
3. Với mức cần duyệt (kết thúc (b)), hệ thống đặt đơn ở "Chờ duyệt chiết khấu", gửi yêu cầu cho người duyệt và chưa ghi đơn vào ERP.
4. Việc duyệt thuộc F5 (use case riêng, chưa có mã). Sau khi duyệt, đơn tiếp tục từ bước 7a `[GIẢ ĐỊNH]`.

**A2 Lưu nháp** (tại bước 6) → kết thúc với đơn "Nháp"
1. Đại lý chọn "Lưu nháp".
2. Hệ thống lưu đơn đang soạn ở trạng thái "Nháp", không kiểm tra công nợ, không ghi vào ERP.
3. Hệ thống thông báo đã lưu. Đại lý mở lại đơn nháp để tiếp tục từ bước 3 `[GIẢ ĐỊNH]`.

### 7. Exception flows
Case gốc chỉ có E1, E2. E3, E4, E5 do BA đề xuất để đủ tối thiểu 3 exception, đều gắn `[GIẢ ĐỊNH]`.

**E1 Không đủ tồn kho** (tại bước 3) → quay lại bước 3
1. Hệ thống không nhận số lượng vượt tồn và hiển thị tồn kho hiện có của sản phẩm.
2. Đại lý giảm số lượng hoặc bỏ sản phẩm. Không hỗ trợ đặt vượt tồn `[GIẢ ĐỊNH]`.

**E2 Quá hạn công nợ** (tại bước 7, ở 7a) → kết thúc với đơn "Chờ kế toán xử lý"
1. ERP báo đại lý quá hạn công nợ.
2. Hệ thống không ghi đơn vào ERP, giữ đơn ở trạng thái "Chờ kế toán xử lý" (giữ tại cổng `[GIẢ ĐỊNH]`).
3. Hệ thống thông báo cho Kế toán có đơn bị giữ (qua Email `[GIẢ ĐỊNH]`).
4. Hệ thống hiển thị cho đại lý rằng đơn chưa được xác nhận và đang được xử lý, không nêu số công nợ `[GIẢ ĐỊNH]`.

**E3 ERP không phản hồi khi ghi đơn** (tại bước 7) → kết thúc với đơn "Nháp" `[GIẢ ĐỊNH]`
1. Hệ thống không nhận phản hồi từ ERP trong thời gian chờ tối đa (giá trị chưa chốt) khi kiểm tra công nợ (7a) hoặc ghi đơn (7b).
2. Hệ thống không xác nhận đơn, chuyển đơn về "Nháp" và báo đại lý thử lại sau.
3. Trước khi gửi lại ở 7b, hệ thống kiểm tra đơn đã có trong ERP hay chưa để không tạo đơn trùng.

**E4 Mất kết nối khi đại lý gửi đơn** (tại bước 6) → kết thúc với đơn "Nháp" `[GIẢ ĐỊNH]`
1. Yêu cầu gửi đơn của đại lý không tới được hệ thống; thiết bị hiển thị lỗi kết nối.
2. Khi có lại kết nối, đại lý mở lại đơn đã lưu tự động ở "Nháp" và gửi lại từ bước 6; hệ thống chặn gửi trùng.

**E5 ERP không phản hồi khi tải danh mục, giá, tồn kho** (tại bước 2) → use case dừng `[GIẢ ĐỊNH]`
1. Hệ thống không nhận phản hồi từ ERP trong thời gian chờ tối đa.
2. Hệ thống báo chưa tải được danh mục và đề nghị thử lại sau. Chưa có đơn nên không có trạng thái "Nháp".

### 8. Business rules và truy vết
Mã BR-C do repo ba-skills đặt để truy vết (case gốc không đánh mã nhóm rule này); ngưỡng chiết khấu là `[GIẢ ĐỊNH]`.

| Mã | Nội dung | Áp dụng tại | Nguồn |
|---|---|---|---|
| BR-C1 | Dưới 5% đại lý tự áp · 5% đến 10% TP Quản lý kênh duyệt · trên 10% Giám đốc Kinh doanh duyệt | A1 | Case `[GIẢ ĐỊNH]` ngưỡng |
| BR-C2 | Giá niêm yết và tồn kho luôn lấy từ ERP; trên cổng không ai sửa | Bước 2, 5; E1 | Case, R6 |
| BR-C3 | Chiết khấu tính trên giá niêm yết, áp cho cả đơn | Bước 5; A1 | Case |
| BR-C4 | Mỗi lần xin chiết khấu phải có lý do | A1 | Case |
| BR-C5 | Quyết định duyệt hoặc từ chối lưu kèm người duyệt và thời điểm | A1 (thực hiện ở F5) | Case, R7 |
| BR-C6 | Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP | A1; bước 7b | Case |
| BR-C7 | Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo | E2 (7a) | Case, R11 |

Truy vết: R1, R2, R5, R6, R11 → UC-01 (bước 1-8, E2) · R7 → A1 (BR-C5, lưu vết ở F5) · F3 → UC-01 · F5 → A1 · Bước sau: US-xx, AC-xx trích dẫn mã bước và luồng ở trên.

### Câu hỏi mở
1. Đơn "Chờ kế toán xử lý" được giữ ở cổng hay đã ghi vào ERP với trạng thái riêng? Kế toán có những lựa chọn nào và use case xử lý đó có mã gì? (Chị Loan)
2. Có cho đặt vượt tồn kho (đặt trước) không, hay luôn chặn như E1? (Chị Hạnh)
3. Chiết khấu dưới 5% tự áp có cần lý do và lưu người áp không? Sau khi duyệt, đơn có tự đi tiếp từ bước 7a không, hay đại lý phải gửi lại? (Chị Hạnh, Anh Quang)
4. Case gốc chỉ có E1, E2; E3, E4, E5 do BA đề xuất `[GIẢ ĐỊNH]`: có đưa vào phạm vi Phase 1 không, thời gian chờ ERP là bao lâu, và ERP có cơ chế chống tạo đơn trùng không? (Anh Kiên, Chị Loan, dev)
5. E3 hiện gộp trường hợp ERP không phản hồi ở 7a và 7b; nếu ERP xử lý hai lệnh này khác nhau thì có cần tách thành hai exception không? (Chị Loan, dev)
6. Cổng chạy trên điện thoại mạng yếu (R5, R12): có cần lưu nháp tự động trước khi gửi (E4) không? (Anh Nhân, Chị Hạnh)
