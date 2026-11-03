## Phân tích business rule: Báo dự án, đặt hàng và chiết khấu (Phase 1)
**Nguồn:** BR-D1…D5, BR-C1…C7, BR-P1, R4, R9, R11, UC-01 (bước 5, 7, A1, E2) · **Phạm vi:** 13 rule (5 rule báo dự án, 7 rule đặt hàng/chiết khấu, 1 rule phân quyền) · **Giới hạn:** BR-P1 là `[GIẢ ĐỊNH]` và chưa có văn bản nên chỉ phân tích ở mức mô tả; chủ sở hữu rule không được nêu trong đầu vào
Mã BR-C và BR-P do repo đặt để truy vết (không phải mã của case gốc); BR-D là mã của case.

### 1. Bảng rule
| Mã | Phát biểu rule | Loại | Kiểu (nếu Behaviour) | Nguồn | Chủ sở hữu | Ghi chú |
|---|---|---|---|---|---|---|
| BR-D1 | Hai dự án là trùng khi giống nhau đồng thời ở cả ba thuộc tính: tên dự án, chủ đầu tư, tỉnh/thành. | Definition | — | Rule báo dự án | chưa rõ | Tiêu chí "giống" chưa xác định, xem GAP-01 |
| BR-D2 | Dự án chỉ được bảo hộ sau khi TP Quản lý kênh duyệt. | Behaviour | Điều kiện–hành động | Rule báo dự án | chưa rõ | Xem GAP-02 |
| BR-D3 | Bảo hộ có hiệu lực 90 ngày kể từ ngày duyệt `[GIẢ ĐỊNH]`. | Behaviour | Điều kiện–hành động | Rule báo dự án | chưa rõ | Lưỡng tính: cũng có thể coi là một phần định nghĩa "bảo hộ". Xếp Behaviour vì là ràng buộc thời hạn; BA chốt. Xem GAP-02 |
| BR-D4 | Nếu đại lý báo dự án trùng với dự án đang được bảo hộ thì hệ thống thông báo cho đại lý báo sau là bị trùng. | Behaviour | Điều kiện–hành động | Rule báo dự án | chưa rõ | Xem X-02, X-03 |
| BR-D5 | Đại lý chỉ được xem dự án do chính đại lý đó báo. | Behaviour | Cấm | Rule báo dự án | chưa rõ | Chưa nói áp cho vai nào, xem X-01 |
| BR-C1 | Chiết khấu dưới 5%: đại lý tự áp; từ 5% đến 10%: TP Quản lý kênh duyệt; trên 10%: Giám đốc Kinh doanh duyệt. | Behaviour | Điều kiện–hành động | Case, rule đặt hàng và chiết khấu | chưa rõ | Rule bảng quyết định: gộp 3 mức vào một rule, bảng ở mục 2. Ngưỡng 5%, 10% `[GIẢ ĐỊNH]`. Xem X-04, GAP-03 |
| BR-C2 | Giá niêm yết và tồn kho luôn lấy từ ERP, trên cổng không ai sửa. | Behaviour | Bắt buộc | Case, rule đặt hàng và chiết khấu (R6) | chưa rõ | Khớp R6 |
| BR-C3 | Chiết khấu được tính trên giá niêm yết và áp cho cả đơn. | Definition | — | Case, rule đặt hàng và chiết khấu | chưa rõ | Định nghĩa cách tính chiết khấu |
| BR-C4 | Mỗi lần xin chiết khấu phải có lý do. | Behaviour | Bắt buộc | Case, rule đặt hàng và chiết khấu | chưa rõ | Xem X-04 |
| BR-C5 | Quyết định duyệt hoặc từ chối chiết khấu được lưu kèm người duyệt và thời điểm. | Behaviour | Bắt buộc | Case, rule đặt hàng và chiết khấu (R7) | chưa rõ | Xem X-04. Khớp R7 (lưu vết duyệt) |
| BR-C6 | Đơn chưa được duyệt chiết khấu thì chưa được ghi vào ERP. | Behaviour | Cấm | Case, rule đặt hàng và chiết khấu | chưa rõ | Xem GAP-05 |
| BR-C7 | Nếu đại lý quá hạn công nợ thì đơn bị giữ lại và Kế toán được thông báo. | Behaviour | Điều kiện–hành động | Case, rule đặt hàng và chiết khấu (R11) | chưa rõ | "quá hạn" chưa định nghĩa, xem GAP-04, GAP-05 |
| BR-P1 | Quyền xem dữ liệu được phân theo vùng. | Behaviour | Cho phép | Case, nguyên tắc phân quyền (chưa có văn bản) | chưa rõ | `[GIẢ ĐỊNH]`. Nội dung chỉ có một câu, chưa nói áp cho vai nào. Xem X-01 |

### 2. Bảng quyết định
Áp cho BR-C1 (rule bảng quyết định). Mức tính trên giá niêm yết, cho cả đơn (BR-C3). Ngưỡng `[GIẢ ĐỊNH]`.

| Mức chiết khấu | Ai xử lý | Ghi chú |
|---|---|---|
| Dưới 5% | Đại lý tự áp | Không qua duyệt |
| Từ 5% đến 10% | TP Quản lý kênh duyệt | 5% và 10% đều rơi vào hàng này nếu "5%–10%" hiểu là gồm hai đầu. Theo quy ước đầu mút `[GIẢ ĐỊNH]` trong case, chờ trainer xác nhận |
| Trên 10% | Giám đốc Kinh doanh duyệt | 10% đúng không thuộc hàng này |

### 3. Mâu thuẫn giữa các rule
| ID | Vế A | Vế B | Mức mâu thuẫn | Tình huống làm lộ | Phương án giải quyết | Ai quyết |
|---|---|---|---|---|---|---|
| X-01 | R9: sales khu vực xem hết đơn và dự án của mọi đại lý, cả vùng khác | BR-D5 và BR-P1 (phân quyền theo vùng) | Trực tiếp hoặc gián tiếp, tùy BR-D5 áp cho vai nào | Sales khu vực của một vùng mở danh sách dự án và thấy dự án do đại lý vùng khác báo. Hiểu (a): BR-D5 chỉ áp cho đại lý, thì R9 không trái chữ BR-D5 nhưng trái BR-P1. Hiểu (b): BR-D5 áp cho mọi vai, thì R9 trái trực tiếp. Lưu ý BR-D2 buộc TP Quản lý kênh phải xem dự án của mọi đại lý để duyệt, nên (b) khó đúng nguyên văn; BA xác nhận | (1) BR-D5 chỉ áp cho đại lý, thêm rule quyền xem riêng cho sales khu vực theo vùng (cụ thể hóa BR-P1), thu hẹp R9. (2) Giữ R9, bỏ BR-P1 đối với sales, kèm giới hạn chỉ đọc. (3) Sales xem mọi vùng nhưng ẩn bớt thuộc tính nhạy cảm của đại lý khác | Anh Quang (nêu R9), Chị Hạnh (quản lý kênh), Anh Kiên (phân quyền) |
| X-02 | BR-D4: thông báo cho đại lý báo sau là bị trùng | BR-D5: đại lý chỉ xem dự án do mình báo | Gián tiếp | Đại lý B báo dự án đang được bảo hộ và nhận thông báo "bị trùng". Nếu thông báo nêu đại lý A hay chi tiết dự án thì B biết dự án của A, trái BR-D5. Nếu chỉ nói "bị trùng" thì B vẫn suy ra có dự án đang bảo hộ | (1) Thông báo trung tính: chỉ nói đã có dự án đang bảo hộ, không nêu đại lý hay chi tiết. (2) Chỉ TP Quản lý kênh thấy thông tin trùng, đại lý B nhận "đang xem xét". (3) Cho B thấy tên dự án trùng nhưng không thấy đại lý nào | Chị Hạnh; tham vấn Anh Nhân với vai đại lý |
| X-03 | R4: báo ngay nếu dự án đã có đại lý khác báo | BR-D2 và BR-D4: chỉ báo trùng khi dự án đang bảo hộ | Phạm vi R4 rộng hơn BR-D4 (gián tiếp) | Đại lý A vừa báo dự án và chưa được duyệt, đại lý B báo cùng dự án. Theo R4, B phải được báo ngay. Theo BR-D2 và BR-D4, dự án chưa bảo hộ nên B không bị báo trùng | (1) Thu hẹp R4 theo BR-D4. (2) Mở BR-D4 thêm trường hợp trùng dự án đang chờ duyệt, kèm rule ai được ưu tiên. (3) Giữ cả hai: B nhận thông báo "đã có báo cáo đang chờ duyệt" nhưng chưa bị coi là trùng chính thức | Chị Hạnh |
| X-04 | BR-C1: dưới 5% đại lý tự áp | BR-C4: mỗi lần xin có lý do; BR-C5: lưu kèm người duyệt | Gián tiếp | Đại lý tự áp 3% cho đơn. Tự áp có tính là "xin" không, có phải ghi lý do không? BR-C5 đòi người duyệt nhưng mức này không có người duyệt | (1) BR-C4 và BR-C5 chỉ áp cho mức cần duyệt, dưới 5% không lưu. (2) Mọi mức đều lưu người áp, thời điểm và lý do; với mức dưới 5% người áp là đại lý. (3) Dưới 5% lưu người áp và thời điểm nhưng không bắt lý do | Anh Quang, Chị Hạnh |

### 4. Rule mơ hồ và khoảng trống
| ID | Rule | Vấn đề | Mức độ | Tình huống minh họa | Cần làm rõ với |
|---|---|---|---|---|---|
| GAP-01 | BR-D1 | Chữ "giống" không nói so khớp tuyệt đối hay có chuẩn hóa. Trả lời trực tiếp băn khoăn 1: **BR-D1 như viết không trả lời được** việc khác hoa/thường hoặc khác một ký tự có là trùng không; kết quả phụ thuộc mức so khớp BA chọn (bảng bên dưới). | Cao | Dự án gốc: "Nhà xưởng KCN Alpha - GĐ2" / "Công ty TNHH Beta" / Bắc Ninh `[GIẢ ĐỊNH]`. Thử TP1 đến TP5 trong bảng bên dưới | Chị Hạnh (chủ nghiệp vụ); Anh Kiên hoặc dev về khả thi |
| GAP-02 | BR-D2, BR-D3, BR-D4 | Không rule nào phủ: (a) sau 90 ngày bảo hộ hết hạn, đại lý khác báo lại thì sao; (b) hai đại lý báo cùng dự án khi chưa dự án nào được duyệt, bên nào được duyệt; (c) dự án bị từ chối duyệt có được báo lại không. | Trung bình | Đại lý A báo ngày 01, được duyệt ngày 02; sang ngày 93 đại lý B báo lại cùng dự án `[GIẢ ĐỊNH]` | Chị Hạnh |
| GAP-03 | BR-C1; UC-01 bước 5 | "chiết khấu chuẩn" ở bước 5 chưa có rule định nghĩa; case chỉ quy ước tạm mặc định 0% `[GIẢ ĐỊNH]`. Với đại lý có chuẩn khác 0%, chưa rõ ngưỡng của BR-C1 tính trên tổng (chuẩn cộng phần xin thêm) hay chỉ phần xin thêm. Hai đầu 5% và 10% hiện chỉ dựa trên quy ước đầu mút `[GIẢ ĐỊNH]`. | Trung bình | Giả sử đại lý có chiết khấu chuẩn 3% và xin thêm 4% `[GIẢ ĐỊNH]`: tổng 7% thuộc bậc TP Quản lý kênh duyệt, còn riêng phần thêm 4% thì đại lý tự áp được | Chị Hạnh, Anh Quang |
| GAP-04 | BR-C7; R11 | "quá hạn công nợ" chưa định nghĩa: quá hạn từ mốc nào, trong khi hạn trả chậm là 30–45 ngày tùy hạng `[GIẢ ĐỊNH]` và "hạng" chưa được định nghĩa. Thiếu rule sau khi Kế toán xử lý: đơn được thả hay bị hủy, trong bao lâu. R11 còn hai phương án, BR-C7 khớp phương án "kế toán được báo trước khi đơn vào ERP"; cần xác nhận. | Trung bình | Đại lý hạng trả chậm 30 ngày, hóa đơn ngày 31: quá hạn từ ngày 31 hay ngày 32? `[GIẢ ĐỊNH]` | Chị Loan |
| GAP-05 | BR-C6, BR-C7; UC-01 | Chưa có thứ tự ưu tiên khi một đơn vừa chờ duyệt chiết khấu vừa quá hạn công nợ. Công nợ được kiểm ở bước 7, sau khi gửi đơn; trạng thái hiển thị là "Chờ duyệt chiết khấu" hay "Chờ kế toán xử lý" và đơn phải qua cả hai cửa hay chỉ một. | Trung bình | Đơn có chiết khấu 8% của đại lý đang quá hạn công nợ `[GIẢ ĐỊNH]` | Chị Hạnh, Chị Loan |

**Thử BR-D1 trên dữ liệu giả (trả lời băn khoăn 1; liên quan GAP-01).** Các cặp TP1–TP5 trùng cả hai thuộc tính còn lại với dự án gốc, chỉ khác như ghi. Ba mức so khớp xem `references/rule-patterns.md`.

| Cặp | Khác biệt | A. Khớp tuyệt đối | B. Chuẩn hóa rồi khớp (bỏ mọi khoảng trắng, hoa/thường, dấu) | C. B kèm cờ nghi trùng |
|---|---|---|---|---|
| TP1 | Chỉ khác hoa/thường | Không trùng | Trùng | Trùng |
| TP2 | Thừa một khoảng trắng | Không trùng | Trùng | Trùng |
| TP3 | Đ gõ thành D | Không trùng | Trùng | Trùng |
| TP4 | GĐ2 thành GĐ3 (có thể là dự án khác thật) | Không trùng | Không trùng | Nghi trùng, người xem quyết; có thể cờ nhầm |
| TP5 | Chủ đầu tư viết "Cty" thay "Công ty" | Không trùng | Không trùng | Không trùng |

Đọc bảng: mức A bỏ lọt cả năm cặp, nên nỗi đau "hai đại lý báo trùng" gần như còn nguyên. Mức B bắt TP1–TP3 nhưng lọt TP5. Mức C thêm TP4 nhưng tăng việc duyệt tay và có thể cờ nhầm. Không mức nào bắt TP5; viết tắt cần xử lý riêng (ví dụ chọn chủ đầu tư từ danh mục). Chọn mức nào là quyết định của BA và chủ sở hữu rule.

### 5. Thuật ngữ cần định nghĩa
- dự án trùng / khớp: cách so khớp ba thuộc tính (GAP-01).
- đang bảo hộ, hết hạn bảo hộ: trạng thái nào được tính (GAP-02).
- chiết khấu chuẩn: nguồn và cách xác định (GAP-03).
- quá hạn công nợ: mốc tính (GAP-04).
- hạng đại lý: tiêu chí phân hạng và hạn trả chậm tương ứng (GAP-04).

**Rule sẵn sàng chuyển tiếp** (write-use-case-spec, write-user-story-and-ac): BR-C2, BR-C3, BR-C6. Các rule còn lại chờ giải quyết phát hiện liên quan.

### Câu hỏi mở
1. Chị Hạnh: BR-D1 dùng mức so khớp nào (A, B hay C)? Chủ đầu tư viết tắt như "Cty" xử lý ra sao?
2. Anh Quang, Chị Hạnh, Anh Kiên: BR-D5 áp cho những vai nào, và BR-P1 (phân quyền theo vùng) có văn bản chưa? Sales khu vực xem theo vùng hay toàn quốc, chỉ đọc hay được sửa (X-01)?
3. Chị Hạnh: dự án đang chờ duyệt, hết 90 ngày, hai đại lý báo cùng lúc, và dự án bị từ chối được xử lý thế nào (GAP-02, X-03)?
4. Chị Hạnh, Anh Nhân: thông báo "bị trùng" được phép lộ thông tin gì cho đại lý báo sau (X-02)?
5. Anh Quang, Chị Hạnh: ngưỡng chiết khấu tính trên tổng hay phần xin thêm, "chiết khấu chuẩn" đến từ đâu, và mức dưới 5% có lưu lý do và người áp không (GAP-03, X-04)?
6. Chị Loan: "quá hạn công nợ" tính từ mốc nào, đơn được thả hay hủy sau khi Kế toán xử lý, và thứ tự ưu tiên khi đơn vừa chờ duyệt chiết khấu vừa quá hạn (GAP-04, GAP-05)?
