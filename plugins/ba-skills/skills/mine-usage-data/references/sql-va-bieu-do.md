# Tham khảo: SQL, biểu đồ và đối chiếu số

## 1. Quy ước viết SQL trong skill
- Dialect mặc định: PostgreSQL. Dòng đầu mỗi khối ghi rõ dialect và định nghĩa lọc.
- Tính khoảng thời gian trong một CTE duy nhất (cột `gio`) để chỉ phải đổi một dòng khi sang dialect khác.
- Ép kiểu `::numeric` trước `ROUND(..., n)`; `PERCENTILE_CONT` trả về `double precision`.
- So sánh với ngưỡng bằng `<=` hay `<` phải khớp cách mục tiêu được phát biểu ("trong 4 giờ" thường là `<=`).
- Giờ ngược thứ tự (`confirmed_at < created_at`) và `NULL` loại khỏi phép tính thời gian, nhưng phải đếm và báo ở M0.

## 2. Đổi dialect

| Việc | PostgreSQL | MySQL | SQL Server | BigQuery |
|---|---|---|---|---|
| Số giờ giữa hai mốc | `EXTRACT(EPOCH FROM (b - a)) / 3600.0` | `TIMESTAMPDIFF(SECOND, a, b) / 3600.0` | `DATEDIFF(SECOND, a, b) / 3600.0` | `TIMESTAMP_DIFF(b, a, SECOND) / 3600.0` |
| Đếm có điều kiện | `COUNT(*) FILTER (WHERE x)` | `SUM(x)` hoặc `SUM(CASE WHEN x THEN 1 END)` | `SUM(CASE WHEN x THEN 1 ELSE 0 END)` | `COUNTIF(x)` |
| Trung vị | `PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY gio)` | không có sẵn, dùng `ROW_NUMBER` | `PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY gio) OVER (PARTITION BY ...)` | `PERCENTILE_CONT(gio, 0.5) OVER (...)` |
| Tổng theo nhóm kèm dòng tổng | `GROUP BY ROLLUP (c)` | `GROUP BY c WITH ROLLUP` | `GROUP BY ROLLUP (c)` | `GROUP BY ROLLUP (c)` |

## 3. Truy vấn chất lượng dữ liệu (M0) nên có
- Tổng dòng và số khóa duy nhất (phát hiện trùng).
- Số dòng nháp hoặc hủy: dòng hợp lệ nhưng ngoài mẫu số "đơn đã gửi"; đếm riêng, không gọi là lỗi.
- Trạng thái "đã xác nhận" nhưng thiếu giờ xác nhận.
- Giờ xác nhận trước giờ tạo (lệch múi giờ, nhập tay, đồng hồ hệ thống).
- Khoảng ngày thực tế có trong dữ liệu so với giai đoạn đã yêu cầu.

## 4. Chọn biểu đồ

| Loại câu hỏi | Biểu đồ nên dùng | Tránh |
|---|---|---|
| Tỷ lệ theo thời gian | Cột chồng 100% theo ngày/tuần, kèm đường ngang là mục tiêu | Biểu đồ tròn nhiều lát |
| Phân phối thời gian xử lý | Box plot hoặc strip plot theo nhóm, kèm đường ngang là ngưỡng | Chỉ vẽ cột trung bình (che đuôi dài) |
| Danh sách đơn đang giữ | Cột ngang theo số giờ, tô màu theo trạng thái | Biểu đồ đường (không có thứ tự thời gian) |
| Cơ cấu theo đại lý | Cột chồng theo đại lý, gộp nhóm nhỏ vào "Khác" | Hiện tên/mã đại lý khi nhóm dưới 5 dòng |

Cảnh báo chung: ghi cỡ mẫu `n` trên biểu đồ; trục bắt đầu từ 0 với biểu đồ cột; nêu rõ đường mục tiêu là `[GIẢ ĐỊNH]` nếu chưa chốt.

## 5. Đối chiếu số trước khi kết luận
1. Đối chiếu **tổng** trước (số dòng, số đơn trong giai đoạn) rồi mới tới chỉ số.
2. Mỗi dòng đối chiếu có: nguồn, người sở hữu nguồn, tiêu chí khớp (tuyệt đối hay dung sai), trạng thái (Chưa đối chiếu / Khớp / Lệch có giải thích / Lệch chưa giải thích).
3. Lệch chưa giải thích thì dừng kết luận, ghi vào câu hỏi mở.
4. Không thay số của nguồn gốc (ERP) bằng số của bản trích xuất khi hai số khác nhau.
5. Số đã trình bày cho sponsor khi chưa đối chiếu phải kèm nhãn "sơ bộ".
