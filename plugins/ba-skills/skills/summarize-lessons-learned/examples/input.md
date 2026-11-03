# Input mẫu: summarize-lessons-learned

Ghi chú retro hư cấu của case Đại Việt Electric. Toàn bộ sự việc, số liệu, hạn là giả định. Ghi chú gốc còn tên người; skill phải ẩn danh trước khi xử lý.

## Bối cảnh
- Retro sau Sprint 1 của Phase 1 (cổng đại lý + CRM nội bộ), sprint 2 tuần `[GIẢ ĐỊNH]`.
- Phạm vi Sprint 1 `[GIẢ ĐỊNH]`: luồng chính và A1 của UC-01 Đặt hàng (F3), duyệt chiết khấu cơ bản (F5), khung đăng nhập.
- Tham dự retro: BA, Dev A, Dev B, QA, PM. Chị Hạnh (TP Quản lý kênh, key user) dự phần đầu để phản hồi demo.
- Nhóm dùng các skill của ba-skills để AI sinh tài liệu; BA review đầu ra trước khi giao dev.
- Business rule chiết khấu đã có từ trước sprint (BR-C1): dưới 5% đại lý tự áp, 5%–10% TP Quản lý kênh duyệt, trên 10% Giám đốc Kinh doanh duyệt `[GIẢ ĐỊNH]`.

## Ghi chú retro (nguyên văn rút gọn)
**Tốt**
- N1. Chị Hạnh sau demo: luồng đặt hàng "đúng ý, bớt Zalo hơn nhiều".
- N2. Dev A: UC-01 có main flow rõ nên làm luồng chính rất nhanh.
- N3. QA: tên trạng thái đơn (Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận) thống nhất giữa dev và test, khỏi cãi nhau.

**Chưa tốt**
- N4. Dev B: AC của story duyệt chiết khấu ghi "từ 3% cần TP Quản lý kênh duyệt, trên 8% cần Giám đốc", nhưng BR-C1 là 5% và 10%. Code theo AC xong mới phát hiện khi Chị Hạnh test thử lúc demo. Phải sửa logic duyệt và 4 test case. AC này do AI viết, BA review không soát số.
- N5. BA: mockup màn hình tạo đơn do AI sinh có dòng "Chiết khấu trên 12% cần Giám đốc Kinh doanh duyệt". Số 12% không có trong rule. Mình bắt được trước khi giao dev, nhưng đây là lần thứ hai trong sprint AI tự điền ngưỡng.
- N6. QA: test thử khi ERP trả chậm thì đại lý bấm gửi đơn hai lần, sinh hai mã đơn. UC-01 chỉ có E1 (không đủ tồn kho) và E2 (quá hạn công nợ), không có trường hợp ERP không phản hồi hay mất mạng khi gửi đơn. Đây là 1 bug mức cao.
- N7. Dev A: AC của story đặt hàng chỉ có đường chính và "đủ tồn kho". Lúc code phải tự đoán khi hết hàng giữa chừng và khi gửi đơn lỗi. AC này cũng do AI viết.
- N8. QA: sơ đồ trạng thái đơn do AI vẽ thiếu trạng thái "Chờ kế toán xử lý", phát hiện lúc viết test case; BA vẽ bổ sung. Mới thấy một lần.
- N9. BA: trong một AC AI viết lẫn "khách hàng" và "đại lý" cho cùng một đối tượng, Dev A phải hỏi lại. Mới thấy một lần.
- N10. Dev A: chưa có tài liệu kỹ thuật kết nối ERP (Chị Loan chưa gửi, chị chỉ họp 1 buổi/tuần), phải mock ERP, mất khoảng 2 ngày `[GIẢ ĐỊNH]`.
- N11. QA: build đầu tiên cho test đến vào thứ Năm tuần 2, test dồn vào hai ngày cuối, nhiều bug báo muộn.
- N12. PM: Anh Quang hỏi thêm màn hình báo cáo doanh số giữa sprint; đã giải thích thuộc Phase 2 nhưng mất nửa buổi họp.

**Ý tưởng**
- N13. Dev B: BA nên có checklist "mọi con số trong AC phải trỏ tới rule nào" khi review đầu ra AI.
- N14. QA: viết test case từ AC ngay khi AC chốt, không đợi build.

## Yêu cầu của BA
Tổng kết bài học Sprint 1: chủ đề, hành động, và phần lỗi AI lặp lại cần sửa skill trong ba-skills. Ghi chú không nêu tên skill đã sinh từng tài liệu; hãy suy từ loại tài liệu và gắn `[GIẢ ĐỊNH]`.
