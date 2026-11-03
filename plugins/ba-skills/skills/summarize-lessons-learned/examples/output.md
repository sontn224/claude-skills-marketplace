## Tổng kết bài học: Sprint 1, Phase 1 (cổng đại lý)
**Nguồn:** ghi chú retro N1–N14 · **Người tham gia (theo vai trò):** BA, Dev A, Dev B, QA, PM, TP Quản lý kênh (key user, dự phần phản hồi demo) · **Giới hạn:** ghi chú không nêu skill đã sinh từng tài liệu nên skill nguồn được suy từ loại tài liệu `[GIẢ ĐỊNH]`; chưa có log lỗi AI các lần trước nên "lặp lại" chỉ đếm trong Sprint 1. Số lần nhắc đếm theo nhãn của ghi chú (Chưa tốt cho cột Đổi, Tốt cho cột Giữ), ý tưởng không cộng vào; số lần nhắc khác với số lần lặp của lỗi AI ở mục 3. Tên người đã được thay bằng vai trò.

### 1. Chủ đề
| # | Chủ đề | Giữ (tốt) | Đổi (chưa tốt) | Bằng chứng | Số lần nhắc |
|---|---|---|---|---|---|
| TM1 | Con số và ngưỡng trong tài liệu AI sinh không khớp business rule | — | AC và mockup có ngưỡng chiết khấu khác rule; sửa lại logic và test | "ghi 3% và 8% nhưng rule là 5% và 10%" (N4); "số 12% không có trong rule" (N5) | 2 (N4, N5); ý tưởng: N13 |
| TM2 | Tài liệu AI sinh thiếu nhánh lỗi và trạng thái | — | UC và AC thiếu tình huống ERP/mạng lỗi; sơ đồ trạng thái thiếu một trạng thái | "ERP trả chậm thì bấm gửi hai lần sinh hai mã đơn" (N6) | 3 (N6, N7, N8) |
| TM3 | Phụ thuộc ERP khi chưa có tài liệu kỹ thuật | — | Phải mock ERP, mất khoảng 2 ngày `[GIẢ ĐỊNH]` | "chưa có tài liệu kỹ thuật kết nối ERP" (N10) | 1 |
| TM4 | Nhịp test: build đến muộn, test dồn cuối sprint | Ý tưởng viết test case sớm từ AC | Build đầu tiên cho QA đến thứ Năm tuần 2 | "test dồn vào hai ngày cuối" (N11) | 1 (N11); ý tưởng: N14 |
| TM5 | Tài liệu rõ và phản hồi sớm từ key user giúp làm nhanh | Use case có main flow rõ; tên trạng thái thống nhất; demo được key user đồng ý | — | "UC-01 có main flow rõ nên làm luồng chính rất nhanh" (N2) | 3 (N1, N2, N3) |
| TM6 | Yêu cầu phát sinh giữa sprint | — | Bàn thêm báo cáo doanh số giữa sprint, mất nửa buổi họp | "đã giải thích thuộc Phase 2 nhưng mất nửa buổi họp" (N12) | 1 |
| TM7 | Thuật ngữ không nhất quán trong tài liệu | — | Lẫn "khách hàng" và "đại lý" cho cùng một đối tượng | "Dev A phải hỏi lại" (N9) | 1 |

### 2. Hành động
| ID | Hành động | Chủ đề | Vai chịu trách nhiệm | Hạn | Xong khi |
|---|---|---|---|---|---|
| A-01 | Mọi AC và mockup có con số phải ghi rule nguồn (mã BR hoặc `[GIẢ ĐỊNH]`); BA đối chiếu số với bảng rule khi review đầu ra AI | TM1 | BA | Từ đầu Sprint 2 `[GIẢ ĐỊNH]` | 100% AC của Sprint 2 có nguồn cho mỗi con số |
| A-02 | Bổ sung exception cho UC-01: E3 (ERP không phản hồi khi ghi đơn), E4 (mất kết nối khi gửi đơn), E5 (ERP không phản hồi khi tải danh mục), kèm xử lý gửi lặp và AC lỗi tương ứng; xác nhận hướng xử lý với Dev A và QA | TM2 | BA | Đầu Sprint 2 `[GIẢ ĐỊNH]` | UC-01 bản mới có đủ exception, Dev A và QA xác nhận; bug gửi hai lần có test hồi quy |
| A-03 | Xin tài liệu kỹ thuật kết nối ERP từ Kế toán trưởng (chủ ERP) trong buổi họp tuần của họ; nếu chưa có thì chốt ngày hẹn | TM3 | PM | Trước Sprint 3 `[GIẢ ĐỊNH]` | Có tài liệu, hoặc có ngày giao được xác nhận bằng văn bản |
| A-04 | Chốt mốc giao build nội bộ giữa sprint; QA viết test case ngay khi AC chốt | TM4 | Dev A và QA | Sprint 2 `[GIẢ ĐỊNH]` | Build đầu tiên cho QA không muộn hơn giữa sprint; test case có trước build |
| A-05 | Thống nhất cách nhận yêu cầu phát sinh: ghi vào backlog kèm phase, không bàn giữa buổi họp sprint | TM6 | PM và BA | Sprint 2 `[GIẢ ĐỊNH]` | Quy tắc được Giám đốc Kinh doanh (sponsor) đồng ý và áp dụng ở buổi họp tiếp theo |
| A-06 | Xem xét và áp dụng các đề xuất sửa skill ở mục 3 | TM1, TM2, TM7 | Trainer | Sprint 2 `[GIẢ ĐỊNH]` | Skill đã sửa, chạy lại 3 lần, bảng chấm trong `_checklist/skill-quality.md` cập nhật |

### 3. Lỗi AI lặp lại cần sửa skill
| ID | Lỗi AI | Loại lỗi | Xuất hiện ở (từ 2 nơi) | Hậu quả | Skill cần sửa | Đề xuất sửa (mục + nội dung) | Cách kiểm tra lại | Ưu tiên |
|---|---|---|---|---|---|---|---|---|
| S-01 | AI tự điền ngưỡng chiết khấu không có trong business rule | Bịa dữ kiện | (1) AC story duyệt chiết khấu (3% và 8% thay vì 5% và 10% của BR-C1); (2) mockup màn hình tạo đơn ("trên 12%") | Sửa lại logic duyệt và 4 test case; lần thứ hai bắt được ở BA trước khi giao dev | write-user-story-and-ac `[GIẢ ĐỊNH]`; generate-prototype-screens `[GIẢ ĐỊNH]` | Đã đọc SKILL.md đích, nên không đề xuất lặp quy tắc có sẵn mà làm cứng. **write-user-story-and-ac** (đã có: mục 2 đòi BR kèm ngưỡng và nguồn; mục 3 bước 8 và mục 5 đòi `[GIẢ ĐỊNH]` cho số không nguồn; chưa có bước đối chiếu đếm được): mục 3 thêm bước "lập bảng con số trong AC → mã BR nguồn (ví dụ ngưỡng duyệt → BR-C1), đối chiếu từng con số với BR; số nào lệch hoặc không có mã thì thay bằng `[GIẢ ĐỊNH]` và đưa vào Câu hỏi mở"; mục 5 thêm câu "số dòng bảng đối chiếu có bằng số con số trong AC không?". **generate-prototype-screens** (đã có: mục 3 bước 6 gắn `[GIẢ ĐỊNH]` cho dữ liệu minh họa; nhưng cũng đòi thông báo lỗi "nêu số" nên dễ khiến AI tự điền ngưỡng): mục 3 bước 6 sửa thành "nêu số lấy từ AC hoặc BR kèm mã nguồn; không có thì dùng placeholder [ngưỡng theo BR-C1], không điền số"; mục 6 thêm ví dụ sai "ghi trên 12% trong khi BR-C1 là 10%" | Chạy lại `examples/input.md` của hai skill. Chạy thêm một lần cố ý bỏ BR-C1 khỏi đầu vào: AI phải hỏi lại hoặc để trống, không điền số | Cao |
| S-02 | AI chỉ viết đường chính và ngoại lệ hiển nhiên, bỏ qua tình huống ERP hoặc mạng lỗi khi gửi đơn | Thiếu nhánh | (1) UC-01 chỉ có E1 (không đủ tồn kho) và E2 (quá hạn công nợ), thiếu E3, E4, E5; (2) AC story đặt hàng chỉ có đường chính và "đủ tồn kho" | 1 bug mức cao (gửi hai lần sinh hai mã đơn khi ERP chậm); Dev A phải tự đoán khi code | write-use-case-spec `[GIẢ ĐỊNH]`; write-user-story-and-ac `[GIẢ ĐỊNH]` | **write-use-case-spec** (đã có: mục 3 bước 5 đòi tìm exception "hệ thống ngoài lỗi, mất mạng" và tối thiểu 3 exception; bước 7 đề xuất thêm kèm `[GIẢ ĐỊNH]`; còn thiếu quy tắc đếm theo bước): mục 3 thêm "mỗi bước gọi hệ thống ngoài hoặc gửi dữ liệu đi phải có ít nhất một exception không phản hồi hoặc mất kết nối; lập bảng bước → exception"; mục 5 thêm câu "số bước gọi hệ thống ngoài có bằng số bước đã có exception tương ứng không?"; mục 6 thêm ví dụ sai: UC-01 chỉ có E1, E2 mà thiếu E3 (bước 7), E4 (bước 6), E5 (bước 2). **write-user-story-and-ac** (đã có: mục 3 bước 5 đòi AC lỗi cho mỗi exception của spec; chưa có xử lý khi spec thiếu exception): mục 3 thêm "bước gọi hệ thống ngoài mà spec không có exception thì ghi dòng Chưa phủ trong ma trận phủ, đưa vào Câu hỏi mở và gợi ý chạy lại write-use-case-spec" | Chạy lại `examples/input.md` của write-use-case-spec, đối chiếu bảng bước → exception với E3, E4, E5 của case; chạy thêm một lần với spec cố ý bỏ E3 để xem write-user-story-and-ac có ghi Chưa phủ không; chạy 3 lần xem số exception có ổn định | Cao |

### 4. Lỗi AI mới thấy một lần (theo dõi)
| ID | Lỗi | Skill liên quan | Khi nào nâng lên "lặp lại" |
|---|---|---|---|
| O-01 | Sơ đồ trạng thái đơn thiếu "Chờ kế toán xử lý". Cùng loại "Thiếu nhánh" với S-02 nhưng khác kiểu (thiếu trạng thái, không phải exception) | draw-state-diagram `[GIẢ ĐỊNH]` | Khi thêm một sơ đồ hoặc tài liệu khác thiếu trạng thái. Nếu Trainer coi cùng gốc với S-02 thì gộp vào S-02 (khi đó S-02 xuất hiện 3 lần) |
| O-02 | Lẫn "khách hàng" và "đại lý" cho cùng một đối tượng trong một AC | write-user-story-and-ac `[GIẢ ĐỊNH]` (hoặc build-glossary nếu glossary không được đưa vào làm đầu vào) | Khi lẫn thuật ngữ xuất hiện ở tài liệu thứ hai |

### Câu hỏi mở
1. Trainer: khi AI sinh AC và mockup, business rule chiết khấu có nằm trong đầu vào không? Ghi chú không nói. Nếu không có thì lỗi S-01 một phần thuộc cách dùng skill, và đề xuất sửa cần kèm hướng dẫn nhập đầu vào.
2. Trainer: sơ đồ trạng thái O-01 và mockup S-01 thật sự do skill nào sinh? Ghi chú chỉ nói "AI vẽ" và "AI sinh".
3. Trainer: O-01 có nên gộp vào S-02 (cùng loại "Thiếu nhánh") hay giữ riêng?
4. QA: Sprint 1 có tổng cộng bao nhiêu bug, bao nhiêu bug bắt nguồn từ tài liệu AI sinh? Cần để đo hiệu quả sau khi sửa skill.
5. PM: các hạn Sprint 2 và Sprint 3 ở mục 2 là ước lượng; chốt ngày thật với ai?
6. PM, Kế toán trưởng (chủ ERP): ngày nào có thể nhận tài liệu kỹ thuật kết nối ERP?
