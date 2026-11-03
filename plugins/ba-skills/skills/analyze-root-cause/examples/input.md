# Input mẫu: analyze-root-cause (Đại Việt Electric, sau go-live Phase 1)

## Yêu cầu của BA
Phase 1 đã go-live. Hãy tìm nguyên nhân gốc vì sao đơn của đại lý bị giữ rất lâu ở trạng thái "Chờ kế toán xử lý", trong khi R1 đặt mục tiêu xác nhận đơn trong 4 giờ. Chỉ phân tích nguyên nhân, chưa đề xuất giải pháp.

## Bối cảnh `[GIẢ ĐỊNH]`
- Go-live Phase 1: thứ Hai 07/12/2026. Sự cố được ghi nhận tuần 14/12 đến 18/12/2026. Giờ Việt Nam.
- Mô tả vấn đề (ticket INC-014 do sales admin tạo): "Hai đơn bị giữ ở Chờ kế toán xử lý từ 15/12 và 17/12. Tính đến 17:00 ngày 18/12 vẫn chưa được nhả. Đại lý gọi hỏi tình trạng đơn."
- Số giờ đã giữ tính đến 18/12 17:00: DH-2026-000105 giữ 78.7 giờ, DH-2026-000113 giữ 31.7 giờ (cùng nguồn dữ liệu ẩn danh với bảng `orders_anon`). Đây là toàn bộ đơn ở trạng thái này trong tuần theo ticket; chưa có dữ liệu các tuần khác.
- Rule liên quan (case): đại lý quá hạn công nợ thì đơn bị giữ lại và Kế toán được thông báo (E2 của UC-01; R11 nêu hai phương án: không cho đặt đơn mới, hoặc báo kế toán trước khi đơn vào ERP).
- Ràng buộc lịch từ case: Kế toán trưởng họp 1 buổi/tuần. Đây chỉ là ràng buộc về lịch, chưa phải bằng chứng về nguyên nhân.
- UC-01 chỉ định nghĩa việc chuyển sang "Chờ kế toán xử lý" và thông báo cho Kế toán; không nêu thời hạn xử lý, người phụ trách hay cơ chế nhắc/leo thang `[GIẢ ĐỊNH: spec chưa có]`.
- Mục tiêu so sánh: R1, xác nhận đơn trong 4 giờ `[GIẢ ĐỊNH]`.

## Log đã ẩn danh
Đoạn trích lọc theo `order_id` từ log ứng dụng cổng và ERP (hư cấu `[GIẢ ĐỊNH]`). Không có số tiền, tên, liên hệ. Chưa kèm log truy cập/thao tác của người dùng phía kế toán.

```
2026-12-15 10:20:41 INFO  portal.order.submit      order_id=DH-2026-000105 dealer=DL-c40e channel=PORTAL
2026-12-15 10:20:42 INFO  erp.credit_check         order_id=DH-2026-000105 dealer=DL-c40e result=OVERDUE
2026-12-15 10:20:42 INFO  portal.order.status      order_id=DH-2026-000105 from=SUBMITTED to=CHO_KE_TOAN_XU_LY
2026-12-15 10:20:43 INFO  notify.email.send        order_id=DH-2026-000105 template=ORDER_HELD_ACCOUNTING to=hop-thu-ke-toan result=SENT
2026-12-17 09:20:12 INFO  erp.order.create_manual  order_id=DH-2026-000113 dealer=DL-a07f channel=EMAIL_ZALO entered_by=SALES_ADMIN_01
2026-12-17 09:20:13 INFO  erp.credit_check         order_id=DH-2026-000113 dealer=DL-a07f result=OVERDUE
2026-12-17 09:20:13 INFO  erp.order.status         order_id=DH-2026-000113 to=CHO_KE_TOAN_XU_LY
2026-12-17 09:20:14 INFO  notify.email.send        order_id=DH-2026-000113 template=ORDER_HELD_ACCOUNTING to=hop-thu-ke-toan result=SENT
2026-12-18 17:00:00 INFO  report.pending_orders    status=CHO_KE_TOAN_XU_LY count=2 oldest=DH-2026-000105
```

## Việc cần làm
Chọn phương pháp phù hợp (5 Whys hoặc xương cá), dựng sơ đồ và danh sách nguyên nhân cần kiểm chứng. Nguyên nhân chỉ là giả thuyết.
