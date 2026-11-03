## Workshop: Chốt rule báo dự án và phạm vi xem dữ liệu
**Mục tiêu:** chốt BR-D1 đến BR-D5 và gỡ mâu thuẫn R9 với BR-D5 · **Kết quả mong đợi:** cuối buổi có QĐ-01 đến QĐ-04 ở trạng thái "Đã chốt" hoặc "Chuyển người quyết" kèm hạn · **Thời lượng / hình thức:** 120 phút, họp hybrid: văn phòng công ty `[GIẢ ĐỊNH]`, anh Nhân (Đà Nẵng) dự online

### Người dự và vai trò
| Tên | Vai trong dự án | Vai trong workshop | Dự phần nào | Lưu ý |
|---|---|---|---|---|
| BA | Phân tích nghiệp vụ | Facilitator | Cả buổi | Không đưa ý kiến về nội dung rule |
| Scribe `[GIẢ ĐỊNH]` | Thành viên nhóm dự án | Scribe và timekeeper | Cả buổi | Ghi theo mẫu quyết định, không diễn giải |
| Chị Hạnh | TP Quản lý kênh, key user | SME và decision owner cho QĐ-01, QĐ-02, QĐ-03 | Cả buổi | Nêu kết luận trước rồi mới kể ví dụ để kịp ghi; ngoại lệ ghi thành dòng riêng |
| Anh Quang | Giám đốc Kinh doanh, sponsor | Decision owner cho QĐ-04 và trọng tài khi chị Hạnh và sales khu vực bất đồng | Cả buổi | Yêu cầu phát sinh ghi vào parking lot; nhắc R10 và F8 đã out of scope |
| Anh Nhân | Chủ đại lý Nhân Phát | Đại diện đại lý | Phút 0–60 | Rời trước phần R9 vì liên quan phạm vi xem dữ liệu đại lý; phần thảo luận rule dùng tình huống cụ thể, không dùng thuật ngữ hệ thống |
| Anh Kiên | Quản trị hệ thống | SME phân quyền | Phút 0–10 và 60–105 | Ghi nhận ràng buộc phân quyền |
| Đại diện sales khu vực `[GIẢ ĐỊNH]` | Người dùng nội bộ | Đại diện sales | Phút 10–105 | Cần chọn người trước; là bên nêu nhu cầu đứng sau R9 |

### Agenda
| Thời gian | Nội dung | Kỹ thuật | Phụ trách | Đầu ra |
|---|---|---|---|---|
| 0–10 | Mở buổi: mục tiêu, luật chơi, cách chốt quyết định | Trình bày | Facilitator | Mọi người đồng ý mục tiêu |
| 10–30 | Hiện trạng: kể một dự án bị báo trùng gần đây | Kể chuyện có hướng dẫn | Chị Hạnh, anh Nhân | Danh sách tình huống trùng thực tế |
| 30–50 | BR-D1 (tiêu chí trùng) và BR-D4 (thông báo khi trùng) | Thử rule trên tình huống ở bước trước | Facilitator | QĐ-01 |
| 50–60 | BR-D2 và BR-D3 (duyệt, thời hạn bảo hộ) | Thảo luận có người quyết | Chị Hạnh | QĐ-02, QĐ-03 |
| 60–70 | Nghỉ và đệm bù giờ; anh Nhân rời buổi | | | |
| 70–95 | R9 so với BR-D5: ai được xem gì, phạm vi vùng | Ghi ý riêng ra giấy, đọc lần lượt, so với phân quyền theo vùng | Facilitator, anh Kiên | Các phương án và ràng buộc |
| 95–105 | Chốt R9 so với BR-D5 | Quyết định của decision owner | Anh Quang | QĐ-04 |
| 105–112 | Đọc lại parking lot, gán việc theo sau và hạn | Rà soát | Scribe | Danh sách việc theo sau |
| 112–120 | Đệm | | | |

Tổng 120 phút. Đệm: phút 60–70 (nghỉ, bù giờ) và 112–120, tổng 18 phút (15 phần trăm).

### Luật chơi và parking lot
- Mỗi người nói tối đa 3 phút mỗi lượt; hết giờ thì ghi vào parking lot kèm người nhận.
- Chưa đạt đồng thuận sau 5 phút thì chuyển decision owner chốt; chưa chốt được thì ghi "Chuyển người quyết" và hạn.
- Yêu cầu mới (ví dụ R10, F8) chỉ ghi vào parking lot, không bàn trong buổi.
- Dữ liệu dự án của từng đại lý không công bố tên trước mặt đại lý khác.

### Chuẩn bị trước
| Ai | Việc | Hạn |
|---|---|---|
| Chị Hạnh | Gửi 3 tình huống báo trùng gần đây, đã bỏ tên đại lý | 2 ngày trước buổi `[GIẢ ĐỊNH]` |
| BA | Gửi pre-read: BR-D1 đến BR-D5 và R9 (1 trang) | 2 ngày trước buổi |
| Anh Kiên | Nêu nguyên tắc phân quyền theo vùng hiện hành (BR-P1) | 1 ngày trước buổi |
| Anh Quang | Cho biết mục đích thực sự của R9 (xem để làm gì) | Trước buổi |
| BA | Chọn và mời đại diện sales khu vực | Ngay |

### Mẫu ghi quyết định
| Mã | Vấn đề | Phương án | Quyết định | Người quyết | Căn cứ | Việc theo sau (ai, hạn) | Trạng thái |
|---|---|---|---|---|---|---|---|
| QĐ-01 | Tiêu chí hai bản báo là một dự án (BR-D1 đang giả định: giống cả ba: tên, chủ đầu tư, tỉnh/thành) và cách thông báo (BR-D4) | | | Chị Hạnh | Tình huống thực tế ở bước 10–30 | | Chưa họp |
| QĐ-02 | Mọi dự án cần TP Quản lý kênh duyệt mới có bảo hộ (BR-D2) | | | Chị Hạnh | | | Chưa họp |
| QĐ-03 | Thời hạn và điểm bắt đầu bảo hộ (BR-D3 đang giả định 90 ngày từ ngày duyệt) và gia hạn | | | Chị Hạnh | | | Chưa họp |
| QĐ-04 | Sales khu vực xem dự án và đơn: R9 (mọi đại lý, mọi vùng) so với BR-D5 và BR-P1 (phân quyền theo vùng `[GIẢ ĐỊNH]`) | A: theo vùng; B: mọi vùng, chỉ xem; C: mọi vùng, ẩn thông tin đại lý | | Anh Quang | R9, BR-D5, BR-P1 (anh Kiên) | | Chưa họp |

### Rủi ro workshop
| Rủi ro | Cách giảm |
|---|---|
| Yêu cầu mới phát sinh trong buổi | Parking lot; nhắc phạm vi trong lời mở; ghi nhận chính thức sau buổi |
| QĐ-01, QĐ-03 chỉ dựa trên kinh nghiệm một phía | Yêu cầu nêu tiêu chí trước, tình huống sau; ghi ngoại lệ thành dòng riêng; đối chiếu với 3 tình huống chị Hạnh gửi trước |
| Đại diện đại lý rời trước phần R9 nên QĐ-04 thiếu tiếng nói đại lý | Gửi kết quả QĐ-04 cho anh Nhân xác nhận sau buổi |
| Quyết định R9 vướng phân quyền | Anh Kiên có mặt để ghi ràng buộc; phương án kỹ thuật tính sau |
| Chưa chọn được đại diện sales khu vực | Hoãn buổi hoặc chuyển QĐ-04 sang buổi sau |

### Phụ lục chỉ BA (không gửi chung)
- Anh Quang hay thêm yêu cầu giữa buổi: nhắc phạm vi ngay lời mở và dùng parking lot.
- Chị Hạnh có xu hướng bảo vệ đại lý lớn: yêu cầu nêu tiêu chí trước, ví dụ sau, để QĐ-01 và QĐ-03 không nghiêng về một nhóm.
- Anh Nhân ngại lộ mối khách và ngại thao tác phức tạp: hỏi bằng tình huống, tránh thuật ngữ hệ thống.
- Anh Kiên quan tâm phân quyền và bảo mật: cho phát biểu sớm ở phần R9 (BR-P1).

### Câu hỏi mở
1. Ai là đại diện sales khu vực, và người đó có quyền nói thay các vùng khác không? (cần: anh Quang)
2. Có số liệu về số lần báo trùng trong 3 tháng gần nhất để chọn mức ưu tiên cho QĐ-01? (cần: chị Hạnh)
3. Mục đích thật của R9 là giám sát hay hỗ trợ khách? Câu trả lời quyết định phương án A, B hay C. (cần: anh Quang)
4. Nếu anh Quang vắng, ai thay làm decision owner cho QĐ-04? (cần: anh Quang)
5. Văn bản chính sách nào đang quy định thời hạn bảo hộ hiện nay, nếu có? (cần: chị Hạnh)
