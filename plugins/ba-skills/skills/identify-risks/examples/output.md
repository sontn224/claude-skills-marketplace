## Risk register: Phase 1, dự án cổng đại lý Đại Việt Electric
Kế hoạch tham chiếu: Phase 1 (3 tháng `[GIẢ ĐỊNH]`), còn 3 sprint x 2 tuần sau Change Request | Thang chấm: mẫu 5x5 (`references/thang-cham-rui-ro.md`) | Ngày: chưa ghi trong đầu vào

Lưu ý: toàn bộ điểm P, I và các vai PM/BA/Tech lead là `[GIẢ ĐỊNH]`, chờ BA/PM xác nhận.

### 1. Nguồn đã dùng
| ID | Tài liệu | Loại nguồn |
|---|---|---|
| S1 | Phạm vi và quyết định mở (trích) | Kế hoạch dự án |
| S2 | Ràng buộc về nguồn lực và quy trình (trích) | Ghi chú stakeholder |
| S3 | Change Request F8, F9 | Yêu cầu thay đổi |
| S4 | Nhu cầu thô và quy tắc liên quan (trích) | Yêu cầu dự án |
| S5 | Nhóm đại lý nòng cốt | Số liệu giả định của case |

### 2. Đánh giá rủi ro
| ID | Loại | Mô tả (Nếu... thì...) | Nguồn | P | I | Điểm | Mức (thang 5x5) | Căn cứ chấm |
|---|---|---|---|---|---|---|---|---|
| RK-01 | Threat | Nếu tài liệu kỹ thuật kết nối ERP không có trước sprint tích hợp thì việc lấy giá, tồn kho và ghi đơn (R2, R6) trễ hoặc phải làm lại | S1, S4 | 4 | 5 | 20 | Rất cao | Tài liệu đã được xác nhận là chưa có; tích hợp là lõi của Phase 1 và chỉ còn 3 sprint |
| RK-02 | Threat | Nếu Kế toán trưởng (chủ ERP) chỉ họp 1 buổi/tuần thì các câu hỏi về ERP và công nợ có thể chờ nhiều tuần mới có trả lời | S2 | 4 | 3 | 12 | Cao | Ràng buộc lịch đã biết; tác động vừa nếu câu hỏi được gom trước |
| RK-03 | Threat | Nếu nền tảng cổng (web tùy biến hay Salesforce) không được chốt kịp thì thiết kế chi tiết, ước lượng và backlog trễ | S1 | 3 | 5 | 15 | Rất cao | Quyết định còn mở; chỉ còn 3 sprint nên trễ quyết định kéo lệch cả phase. Xem câu hỏi mở 1 |
| RK-04 | Threat | Nếu hội nghị đại lý diễn ra đúng lịch mà cổng chưa đủ để giới thiệu thì mất cơ hội thuyết phục đại lý dùng cổng | S3 | 3 | 4 | 12 | Cao | Mốc không dời (S3). Ngày chưa biết nên P chỉ là ước tính |
| RK-05 | Threat | Nếu CR F8 (đa ngôn ngữ, đang ngoài phạm vi) và F9 (SSO cho đại lý, ngoài SSO nhân viên hiện có) được nhận mà không cắt phạm vi hoặc lùi mốc thì Phase 1 trễ hoặc tính năng lõi bị cắt | S1, S3 | 4 | 5 | 20 | Rất cao | Backlog kín, mốc cố định, CR đã được gửi và chờ quyết định (S3) |
| RK-06 | Threat | Nếu ~300 bản ghi đại lý trong Excel và ERP trùng hoặc thiếu hồ sơ nhiều thì import tạo đại lý trùng, đại lý phải đăng ký lại (R8) | S4 | 4 | 3 | 12 | Cao | Nguồn nói hồ sơ hiện trùng, thiếu; 300 bản ghi so với ~200 đại lý ký hợp đồng cho thấy có trùng hoặc bản ghi cũ |
| RK-07 | Threat | Nếu mâu thuẫn R9 và BR-D5 (phạm vi xem theo vùng) không được giải sớm thì mô hình phân quyền phải làm lại, Quản trị hệ thống có thể yêu cầu thiết kế lại vì yêu cầu phân quyền và bảo mật (R7) | S2, S4 | 3 | 4 | 12 | Cao | Mâu thuẫn đã có trong yêu cầu; phân quyền ảnh hưởng nhiều màn hình |
| RK-08 | Threat | Nếu đại lý đang đặt hàng qua điện thoại hoặc Zalo thấy cổng nhiều bước, mạng yếu hoặc chậm cuối tháng nên tiếp tục dùng kênh cũ thì mục tiêu 70% đơn qua cổng (R1) không đạt | S2, S4 | 3 | 4 | 12 | Cao | Ý kiến của một chủ đại lý; R1 là mục tiêu `[GIẢ ĐỊNH]`; chưa có dữ liệu thử nghiệm |
| RK-09 | Opportunity | Nếu mời nhóm đại lý nòng cốt dùng thử tại hội nghị đại lý thì có phản hồi sớm và tăng khả năng dùng cổng | S3, S5 | 3 | 3 | 9 | Trung bình | Số liệu nhóm nòng cốt là giả định; hội nghị là cơ hội đã có lịch |

### 3. Ứng phó và theo dõi
| ID | Chiến lược | Hành động ứng phó | Kế hoạch dự phòng | Trigger | Người phụ trách (vai) | Nhịp review |
|---|---|---|---|---|---|---|
| RK-01 | Mitigate | Gửi yêu cầu chính thức về tài liệu kết nối ERP; đặt buổi làm việc kỹ thuật với chủ ERP; dựng giao diện giả lập ERP để đội làm song song `[GIẢ ĐỊNH]` | Chốt với sponsor phương án tạm cho go-live (ví dụ xuất đơn dạng file cho sales admin) và ghi rõ đánh đổi so với R2 | Cuối sprint hiện tại chưa nhận được tài liệu kết nối ERP | PM `[GIẢ ĐỊNH]` | Hằng tuần |
| RK-02 | Mitigate | Gom câu hỏi gửi trước buổi họp hằng tuần; xin một đầu mối kỹ thuật bên ERP | Chuyển câu hỏi cấp bách lên sponsor để gỡ | Hai buổi họp liên tiếp còn câu hỏi chưa được trả lời | BA `[GIẢ ĐỊNH]` | Hằng tuần |
| RK-03 | Avoid | Đưa quyết định nền tảng lên sponsor kèm bảng so sánh (xem research-benchmark) và hạn chốt rõ | Nếu quá hạn: chọn phương án đội đã sẵn sàng nhất để không dừng thiết kế | Đến hạn chốt mà chưa có quyết định bằng văn bản | PM `[GIẢ ĐỊNH]` | Hằng tuần |
| RK-04 | Mitigate | Lấy ngày hội nghị; xác định phạm vi trình diễn tối thiểu (đặt hàng và theo dõi đơn) | Chuẩn bị bản demo với dữ liệu giả lập | Còn đúng một sprint trước hội nghị mà luồng đặt hàng chưa chạy được | PM `[GIẢ ĐỊNH]` | Mỗi sprint |
| RK-05 | Avoid | Đưa CR qua quy trình thay đổi; phân tích tác động và đề xuất đổi: giữ F8 ngoài phạm vi, đưa F9 sang Phase 2 hoặc bỏ tính năng tương đương | Nếu sponsor bắt buộc: thỏa thuận lùi mốc hoặc cắt tính năng lõi bằng văn bản | CR chưa có quyết định chính thức sau một sprint, hoặc backlog tăng mà không gỡ mục nào | PM `[GIẢ ĐỊNH]` | Hằng tuần |
| RK-06 | Mitigate | Xin mẫu dữ liệu đã ẩn danh sớm; thống nhất quy tắc lọc trùng; chạy thử import trên mẫu | Giữ danh sách bản ghi nghi trùng để xử lý tay trước khi go-live | Mẫu thử import có bản ghi lỗi hoặc trùng vượt ngưỡng do TP Quản lý kênh đặt | TP Quản lý kênh | Mỗi sprint |
| RK-07 | Avoid | Đưa mâu thuẫn R9 và BR-D5 vào một phiên quyết định với sponsor, Quản trị hệ thống và TP Quản lý kênh | Thiết kế phân quyền theo hướng chặt hơn, mở rộng sau khi có quyết định | Bắt đầu thiết kế mô hình phân quyền mà chưa có quyết định | BA `[GIẢ ĐỊNH]` | Hằng tuần |
| RK-08 | Mitigate | Giảm số bước đặt hàng trên điện thoại; thử với nhóm nhỏ trước; hỗ trợ trực tiếp giai đoạn đầu | Giữ kênh đặt hàng cũ có thời hạn, sales admin nhập hộ | Sau hai tuần thử nghiệm, tỷ lệ đơn qua cổng của nhóm thử thấp hơn mức tạm thời sponsor đặt | TP Quản lý kênh | Mỗi sprint |
| RK-09 | Enhance | Mời nhóm đại lý nòng cốt tham gia trình diễn và dùng thử có hướng dẫn | Nếu demo chưa sẵn sàng: ghi nhận phản hồi trên bản mockup | Danh sách đại lý mời được xác nhận trước hội nghị | Giám đốc Kinh doanh | Mỗi sprint |

### 4. Tổng hợp
| Mức | Số rủi ro | ID |
|---|---|---|
| Rất cao (15-25) | 3 | RK-01, RK-03, RK-05 |
| Cao (10-14) | 5 | RK-02, RK-04, RK-06, RK-07, RK-08 |
| Trung bình (5-9) | 1 | RK-09 |
| Thấp (1-4) | 0 | - |

Top rủi ro cần xử lý trước: RK-01 và RK-05 (điểm 20), sau đó RK-03 (15). RK-01 và RK-02 có chung nguyên nhân (phụ thuộc chủ ERP), nên xử lý cùng một đầu mối.

### 5. Điểm chấm thiếu căn cứ
- RK-04: P phụ thuộc ngày hội nghị chưa có trong đầu vào.
- RK-06: P, I dựa trên mô tả định tính; chưa có mẫu dữ liệu thật để đo tỷ lệ trùng.
- RK-08: P dựa trên ý kiến một chủ đại lý; ngưỡng "mức tạm thời" chưa được sponsor đặt.
- Toàn bộ vai PM, BA là vai dự án `[GIẢ ĐỊNH]`; cần đối chiếu đội dự án thật.

### Câu hỏi mở
1. Case ghi backlog đã kín với 3 sprint còn lại nhưng nền tảng cổng vẫn chưa chốt: thời điểm thật của dự án là lúc nào, và đã có phần nào đã xây chưa? (PM, Giám đốc Kinh doanh)
2. Ngày hội nghị đại lý là khi nào, và cổng cần ở trạng thái nào vào ngày đó? (Giám đốc Kinh doanh)
3. Ai bên ERP có thể làm đầu mối kỹ thuật, và tài liệu kết nối dự kiến có khi nào? (Kế toán trưởng)
4. Ngưỡng nào của tỷ lệ bản ghi trùng/lỗi thì chấp nhận được khi import, và tỷ lệ đơn qua cổng tối thiểu của nhóm thử nghiệm là bao nhiêu? (TP Quản lý kênh, Giám đốc Kinh doanh)
5. Các vai PM, BA, Tech lead là những ai trong đội, và họ có đồng ý nhận vai phụ trách rủi ro không? (PM)
