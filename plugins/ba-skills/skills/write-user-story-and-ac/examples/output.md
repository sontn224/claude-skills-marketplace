## User Story và Acceptance Criteria — UC-01 Đặt hàng
Nguồn: UC-01 (main, A1, A2, E1–E5), BR-C1 đến BR-C7, R2 R5 R6 R7 R11 R12, NFR-01 NFR-03 NFR-06 NFR-07 · Trạng thái: Nháp chờ BA verify
Quy ước: mọi giá trị minh hoạ (giá 100.000 đ/cuộn, tồn 20 cuộn) là `[GIẢ ĐỊNH]`; ngưỡng chiết khấu 5% và 10% (BR-C1) là `[GIẢ ĐỊNH]`. Ví dụ tính chiết khấu dùng chiết khấu chuẩn = 0% `[GIẢ ĐỊNH]`. AC không đặt chỉ số hiệu năng: thời hạn dẫn NFR-xx hoặc nằm ở Câu hỏi mở.

### US-01 · Gửi đơn hàng đủ tồn kho
**Là** đại lý, **tôi muốn** thêm sản phẩm vào đơn và gửi đơn, **để** đơn được ghi vào ERP và xác nhận mà không phải gọi hay nhắn Zalo cho sales admin.
- Truy vết: UC-01 main 1–8, E1, E2 · BR-C2, BR-C7 · R2, R5, R6, R11
- INVEST: I ✓ · N ✓ · V ✓ · E ⚠ (cần tài liệu kết nối ERP, chưa có; xem Câu hỏi mở 6) · S ✓ (chiết khấu, nháp, lỗi hạ tầng tách sang US-02 đến US-05) · T ✓

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-01 | Happy | Đại lý đã đăng nhập, tài khoản hoạt động, không quá hạn công nợ; SP-0001 tồn 20 cuộn, giá niêm yết 100.000 đ/cuộn `[GIẢ ĐỊNH]`; đã thêm 5 cuộn SP-0001, đã chọn địa chỉ giao và ngày mong muốn | Gửi đơn | Tổng đơn 500.000 đ; đơn ghi vào ERP trạng thái "Đã xác nhận"; mã đơn hiện trên màn hình; email xác nhận được gửi đến đại lý (thời hạn: Câu hỏi mở 1) | Main 1–8 (7a, 7b) |
| AC-02 | Biên | SP-0001 tồn đúng 20 cuộn | Nhập số lượng 20 | Dòng sản phẩm được thêm, không có cảnh báo thiếu hàng | Main 3 (biên của E1) |
| AC-03 | Lỗi | SP-0001 tồn 20 cuộn | Nhập số lượng 21 | Hiện "Chỉ còn 20 cuộn trong kho" tại dòng sản phẩm; dòng không được tính vào tổng; đơn không gửi được cho đến khi số lượng ≤ 20 | E1 |
| AC-04 | Biên | Đơn đang soạn | Nhập số lượng 0 hoặc để trống | Dòng không được thêm; hiện "Số lượng tối thiểu là 1" `[GIẢ ĐỊNH]` | Main 3 |
| AC-05 | Lỗi | Đại lý quá hạn công nợ theo ERP; đơn hợp lệ | Gửi đơn | Đơn không ghi vào ERP; trạng thái "Chờ kế toán xử lý"; Kế toán nhận thông báo (thời hạn: Câu hỏi mở 1); đại lý thấy "Đơn đang chờ xử lý" và không thấy số tiền công nợ `[GIẢ ĐỊNH]` | E2 (7a) |

### US-02 · Xin chiết khấu thêm cho đơn hàng
**Là** đại lý, **tôi muốn** xin chiết khấu thêm kèm lý do ngay khi soạn đơn, **để** được duyệt đúng người, đúng ngưỡng mà không phải xin qua Zalo.
- Truy vết: UC-01 A1 (bước 5) · BR-C1, BR-C3, BR-C4, BR-C6 · nỗi đau "duyệt chiết khấu qua Zalo, không lưu vết"
- INVEST: I ✓ · N ✓ · V ✓ · E ✓ · S ✓ · T ✓ (ngưỡng BR-C1 còn `[GIẢ ĐỊNH]`)

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-06 | Biên | Đơn tổng niêm yết 500.000 đ; đã nhập chiết khấu 4,9% và lý do | Xác nhận chiết khấu | Chiết khấu áp ngay; tổng đơn 475.500 đ; đơn không chuyển "Chờ duyệt chiết khấu" | A1 (dưới ngưỡng 5%, BR-C1) |
| AC-07 | Biên | Đơn tổng niêm yết 500.000 đ; đã nhập chiết khấu đúng 5,0% và lý do | Gửi đơn | Đơn "Chờ duyệt chiết khấu", người duyệt là TP Quản lý kênh; tổng dự kiến 475.000 đ; đơn chưa ghi vào ERP (BR-C6) | A1 (đúng ngưỡng 5%) |
| AC-08 | Biên | Đơn tổng niêm yết 500.000 đ; đã nhập chiết khấu đúng 10,0% và lý do | Gửi đơn | Đơn "Chờ duyệt chiết khấu", người duyệt vẫn là TP Quản lý kênh (không phải Giám đốc Kinh doanh); tổng dự kiến 450.000 đ; chưa ghi vào ERP | A1 (đúng ngưỡng 10%) |
| AC-09 | Biên | Đơn tổng niêm yết 500.000 đ; đã nhập chiết khấu 10,1% và lý do | Gửi đơn | Đơn "Chờ duyệt chiết khấu", người duyệt là Giám đốc Kinh doanh; tổng dự kiến 449.500 đ; chưa ghi vào ERP | A1 (trên ngưỡng 10%) |
| AC-10 | Lỗi | Đã nhập chiết khấu 7,0%; ô lý do trống hoặc dưới 10 ký tự `[GIẢ ĐỊNH]` | Gửi đơn | Hiện "Nhập lý do xin chiết khấu"; đơn không gửi; không có bản ghi duyệt nào được tạo (BR-C4) | A1 |

### US-03 · Duyệt chiết khấu theo ngưỡng
**Là** TP Quản lý kênh, **tôi muốn** duyệt hoặc từ chối chiết khấu thuộc quyền mình và có lưu vết, **để** kiểm soát mức chiết khấu và có bằng chứng ai duyệt, lúc nào.
- Truy vết: UC-02 (F5, chưa viết) / A1 bước 3 · BR-C1, BR-C5, BR-C6 · R7
- INVEST: I ⚠ (phụ thuộc US-02) · N ✓ · V ✓ · E ✓ · S ✓ · T ✓. Phần của Giám đốc Kinh doanh dùng chung AC-12, không tách story riêng. Khi UC-02 được viết, đối chiếu lại mã luồng.

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-11 | Happy | Đơn "Chờ duyệt chiết khấu" mức 7,0% kèm lý do; TP Quản lý kênh đang xem đơn | Chọn "Duyệt" | Lưu người duyệt và thời điểm duyệt (đến giây) (BR-C5); đại lý nhận email thông báo đã duyệt; đơn tiếp tục kiểm tra công nợ rồi ghi vào ERP, không phải duyệt lại | UC-02 (F5, chưa viết) / A1 bước 3 → Main 7a |
| AC-12 | Lỗi | Đơn "Chờ duyệt chiết khấu" mức 12,0% | TP Quản lý kênh mở đơn | Chỉ xem được, không có thao tác Duyệt; đơn ghi rõ người duyệt cần thiết là Giám đốc Kinh doanh | UC-02 (F5, chưa viết) / A1 bước 3 |
| AC-13 | Lỗi | TP Quản lý kênh đang xem đơn mức 7,0%; chưa nhập lý do từ chối `[GIẢ ĐỊNH]` | Chọn "Từ chối" | Hiện "Nhập lý do từ chối"; không lưu quyết định; trạng thái đơn không đổi | UC-02 (F5, chưa viết) / A1 bước 3 |

### US-04 · Dùng cổng khi mạng yếu hoặc ERP không phản hồi
**Là** đại lý, **tôi muốn** biết rõ và gửi lại an toàn khi mất mạng hoặc ERP chậm, **để** không phải nhập lại đơn và không bị tạo đơn trùng.
- Truy vết: UC-01 E3, E4, E5 (`[GIẢ ĐỊNH]`), Main 2 · R5, R12 · NFR-01, NFR-06, NFR-07
- INVEST: I ✓ · N ✓ · V ✓ · E ⚠ (cần tài liệu ERP) · S ✓ (6 AC) · T ✓

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-14 | Lỗi | Đại lý không quá hạn công nợ, đã gửi đơn hợp lệ; ERP không phản hồi khi kiểm tra công nợ hoặc ghi đơn | Hết thời gian chờ ERP | Hiện "Chưa gửi được đơn, vui lòng thử lại" trong thời hạn theo NFR-06; đơn chuyển "Nháp" với nội dung còn nguyên; hệ thống không báo đơn đã xác nhận | E3 (7a/7b) `[GIẢ ĐỊNH]` |
| AC-15 | Biên | Đơn đã được ERP ghi nhưng không phản hồi nên đang ở "Nháp" (như AC-14) | Gửi lại đơn | Hệ thống kiểm tra ERP trước; ERP chỉ có 1 đơn cho lần đặt này; đại lý thấy mã đơn đã tạo, không có đơn thứ hai | E3 (7b) `[GIẢ ĐỊNH]` |
| AC-16 | Lỗi | Thiết bị đang mất kết nối; đơn hợp lệ | Gửi đơn | Hiện thông báo lỗi kết nối; đơn ở "Nháp" với nội dung còn nguyên (mức bảo toàn theo NFR-07); khi có mạng lại, đại lý mở đơn và gửi lại mà không phải nhập lại | E4 (bước 6) `[GIẢ ĐỊNH]` |
| AC-17 | Biên | Đơn đã tới ERP nhưng thiết bị mất mạng trước khi nhận phản hồi; mạng đã có lại | Gửi lại đúng đơn đó | ERP chỉ có 1 đơn cho lần đặt này; đại lý thấy mã đơn đã tạo, không có đơn thứ hai | E4 (bước 6) `[GIẢ ĐỊNH]` |
| AC-18 | Lỗi | ERP không phản hồi khi tải danh mục, giá, tồn kho | Đại lý chọn "Tạo đơn hàng" | Hiện "Chưa tải được danh mục, vui lòng thử lại" trong thời hạn theo NFR-06; không hiển thị giá hoặc tồn kho; không tạo đơn nào, kể cả "Nháp", vì chưa có đơn | E5 (bước 2) `[GIẢ ĐỊNH]` |
| AC-19 | Happy | Kết nối chậm | Mở "Tạo đơn hàng" | Màn hình hiển thị theo NFR-01; danh mục chưa tải xong thì có chỉ báo đang tải; không hiện giá hoặc tồn kho chưa lấy từ ERP | Main 2 (R12) |

### US-05 · Lưu nháp đơn hàng
**Là** đại lý, **tôi muốn** lưu đơn đang soạn để hoàn tất sau, **để** không mất công chọn lại sản phẩm khi bị gián đoạn.
- Truy vết: UC-01 A2 (bước 6) · R5
- INVEST: I ✓ · N ✓ · V ✓ · E ✓ · S ✓ · T ✓

| AC | Loại | Given | When | Then | Luồng UC |
|---|---|---|---|---|---|
| AC-20 | Happy | Đơn có SP-0001 × 5 và địa chỉ giao | Chọn "Lưu nháp" | Đơn ở trạng thái "Nháp"; không kiểm tra công nợ, không ghi vào ERP; mở lại thấy đủ dòng sản phẩm và địa chỉ | A2 |
| AC-21 | Biên | Đơn chưa có dòng sản phẩm nào | Chọn "Lưu nháp" | Không tạo bản nháp; hiện "Thêm ít nhất 1 sản phẩm" `[GIẢ ĐỊNH]` | A2 |

### Ma trận phủ luồng
| Luồng UC | AC | Ghi chú |
|---|---|---|
| Main 1–8 | AC-01, AC-04, AC-19 | Bước 4 (địa chỉ, ngày mong muốn) mới có AC trong AC-01; chưa có AC biên cho ngày (Câu hỏi mở 7) |
| A1 | AC-06 đến AC-10 | Ngưỡng 5%/10% phủ đủ dưới, đúng, trên |
| A1 (phần duyệt, UC-02 chưa viết) | AC-11 đến AC-13 | Đối chiếu lại khi UC-02 có mã luồng |
| A2 | AC-20, AC-21 | |
| E1 | AC-02, AC-03 | |
| E2 (7a) | AC-05 | |
| E3 (7a/7b) `[GIẢ ĐỊNH]` | AC-14, AC-15 (AC-15 chỉ cho 7b) | Chờ key user công nhận |
| E4 (bước 6) `[GIẢ ĐỊNH]` | AC-16, AC-17 | Chờ key user công nhận |
| E5 (bước 2) `[GIẢ ĐỊNH]` | AC-18 | Chờ key user công nhận |

### Câu hỏi mở
1. Thời hạn hiện mã đơn, gửi email xác nhận và báo Kế toán (AC-01, AC-05) chưa có NFR nào quy định; cần bổ sung vào write-nfr — cần BA và Chị Hạnh, Chị Loan.
2. Ngưỡng 5%/10% tính trên tổng chiết khấu (gồm chiết khấu chuẩn) hay chỉ phần xin thêm (BR-C1, BR-C3)? Đúng 5,0% và đúng 10,0% có thuộc bậc TP Quản lý kênh như đang giả định ở AC-07, AC-08 không? — cần Chị Hạnh, Anh Quang.
3. Đơn bị từ chối chiết khấu chuyển sang trạng thái nào, đại lý có được sửa mức chiết khấu và gửi lại không? Case chưa có trạng thái này — cần Chị Hạnh.
4. Đơn "Chờ kế toán xử lý": đại lý có được biết số tiền công nợ không (AC-05 đang giả định không)? — cần Chị Loan, Chị Hạnh.
5. Tồn kho thay đổi giữa lúc thêm sản phẩm và lúc gửi đơn: có kiểm tra lại tồn kho khi gửi không? Spec mới có E1 tại bước 3 — cần Chị Hạnh, Chị Loan.
6. Tài liệu kỹ thuật kết nối ERP chưa có, nên US-01 và US-04 chưa ước lượng chắc được; thời gian chờ ERP cho E3, E5 cũng chưa chốt (NFR-06 mới nêu thời hạn thông báo) — cần Chị Loan và nhóm kỹ thuật.
7. Ngày giao mong muốn: tối thiểu cách hôm nay mấy ngày? Bản nháp giữ trong bao lâu, tối đa bao nhiêu bản? — cần Chị Hạnh.
