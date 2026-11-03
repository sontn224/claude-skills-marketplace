## Phân tích tài liệu: Hướng dẫn nội bộ "Theo dõi dự án đại lý" (file Excel phòng Quản lý kênh)
**Loại / chủ sở hữu / ngày:** hướng dẫn nội bộ, bản nháp / phòng Quản lý kênh (theo §1) / chưa rõ · **Độ tin cậy:** Thấp đến Trung bình: là bản nháp, không ghi ngày và người duyệt, có mục để trống (§10) · **Mục tiêu đọc:** tìm rule báo dự án, kiểm trùng, bảo hộ, chiết khấu để đối chiếu với BR-D1 đến BR-D5 và ngưỡng chiết khấu đang giả định

### Tóm tắt
Tài liệu mô tả cách phòng Quản lý kênh ghi nhận dự án do đại lý báo vào một file Excel (10 cột, §2). Đại lý gửi qua email hoặc Zalo, nhân viên nhập tay trong 1–2 ngày làm việc (§3). Việc kiểm trùng làm bằng tìm kiếm thủ công theo tên dự án và chủ đầu tư (§4). Trưởng phòng Quản lý kênh duyệt, đại lý giữ dự án khoảng 3 tháng, có ngoại lệ ngầm cho đại lý lớn (§5, §6). Chiết khấu và thông báo trùng đi qua Zalo và điện thoại, gần như không lưu vết (§7, §8).

### Rule trích xuất
| Mã | Rule (diễn đạt lại) | Nguồn | Đối chiếu | Độ rõ |
|---|---|---|---|---|
| RT-01 | Hai dự án là trùng khi giống tên dự án và chủ đầu tư và cùng tỉnh/thành | §4 | = BR-D1 | Rõ về điều kiện; chưa rõ "giống" là khớp từng chữ hay khớp gần đúng |
| RT-02 | Tên gần giống thì hỏi lại đại lý trước khi kết luận trùng | §4 | Mới | Mơ hồ: "gần giống" chưa định nghĩa; ai quyết khi đại lý không trả lời cũng chưa rõ |
| RT-03 | Trưởng phòng Quản lý kênh duyệt dự án | §5 | = BR-D2 | Rõ |
| RT-04 | Sau khi duyệt, đại lý giữ dự án khoảng 3 tháng; hết hạn thì trạng thái "Hết hạn" | §5 | ≈ BR-D3 (90 ngày `[GIẢ ĐỊNH]`); chưa xác nhận | Mơ hồ: "khoảng" |
| RT-05 | Đại lý lớn được gia hạn nếu có lý do | §5 | Mới | Mơ hồ: không nêu ai quyết, gia hạn bao lâu, lý do gì |
| RT-06 | Khi hai đại lý báo trùng, đại lý báo trước (theo Ngày nhận) được giữ | §6 | ≠ BR-D3, BR-D4 (bảo hộ tính từ ngày duyệt, báo sau mới bị thông báo trùng) | Rõ nhưng khác điểm mốc |
| RT-07 | Với đại lý lớn thì "xem xét ưu tiên" khi trùng | §6 | ≠ BR-D4 (không có ngoại lệ cho đại lý lớn) | Mơ hồ |
| RT-08 | Khi trùng, nhân viên gọi điện báo đại lý báo sau | §8 | = BR-D4 về mục đích; kênh điện thoại là cách làm hiện tại | Rõ |
| RT-09 | Chiết khấu thêm trên 8%: hỏi Giám đốc Kinh doanh qua Zalo; ghi quyết định vào Ghi chú nếu nhớ | §7 | ≠ BR-C1 (ngưỡng 5%/10% `[GIẢ ĐỊNH]`) | Rõ về ngưỡng 8%; không có lưu vết bắt buộc (liên quan R7) |

### Thuật ngữ
| Thuật ngữ | Cách tài liệu dùng | Nguồn | Ghi chú |
|---|---|---|---|
| Dự án | Đối tượng đại lý báo, mỗi dòng một dự án | §1, §2 | Chuyển sang build-glossary |
| Chủ đầu tư | Một trong hai trường kiểm trùng, kèm tỉnh/thành là ba | §2, §4 | Chưa nói cách ghi tên (viết tắt, tên đầy đủ) |
| Trùng | Trạng thái khi khớp tên, chủ đầu tư, tỉnh/thành | §2, §4 | Khớp BR-D1 |
| Duyệt | Việc của Trưởng phòng Quản lý kênh với dự án; "hỏi" Giám đốc Kinh doanh với chiết khấu | §5, §7 | Dùng cho hai việc khác nhau |
| Hết hạn | Trạng thái khi quá thời gian giữ dự án | §5 | Tương ứng hết thời hạn bảo hộ |
| Đại lý lớn | Nhóm được gia hạn và xem xét ưu tiên | §5, §6 | Dùng mà không định nghĩa |
| Ngày nhận / Ngày duyệt | Hai mốc ngày; Ngày nhận dùng xét ưu tiên khi trùng (§6) | §2, §6 | Mốc nào tính bảo hộ chưa rõ |
| Mã ĐL | Mã đại lý do phòng tự đặt | §2, §9 | Chưa đối chiếu với mã đại lý trong ERP |

### Mâu thuẫn và chỗ thiếu
| Mã | Loại | Mô tả | Nguồn | Hỏi ai |
|---|---|---|---|---|
| GAP-01 | Mâu thuẫn | Ưu tiên khi trùng tính theo Ngày nhận (§6) hay theo bảo hộ từ ngày duyệt (BR-D3, BR-D4) | §6 so với BR-D3, BR-D4 | Chị Hạnh |
| GAP-02 | Mâu thuẫn | Đại lý lớn có ngoại lệ ngầm ở §5 và §6; BR-D4 không có ngoại lệ | §5, §6 | Chị Hạnh, anh Quang |
| GAP-03 | Mâu thuẫn | Ngưỡng chiết khấu thực tế là trên 8% hỏi Giám đốc; BR-C1 giả định trên 10% do Giám đốc duyệt | §7 | Chị Hạnh, anh Quang |
| GAP-04 | Mơ hồ | "Khoảng 3 tháng" tính từ ngày nào, có đúng 90 ngày không, gia hạn mấy lần | §5 | Chị Hạnh |
| GAP-05 | Thiếu | Mục báo bổ sung thông tin dự án để trống | §10 | Chị Hạnh |
| GAP-06 | Thiếu | Mã ĐL chưa đối chiếu ERP, ảnh hưởng import khoảng 300 đại lý (R8) | §9 | Chị Hạnh, chị Loan |
| GAP-07 | Thiếu | Không có chủ sở hữu, ngày cập nhật, người duyệt tài liệu | Toàn tài liệu | Chị Hạnh |
| GAP-08 | Thiếu | Không có cột lý do xin chiết khấu, người duyệt, thời điểm duyệt (BR-C4, BR-C5, R7) | §2, §7 | Anh Kiên, chị Hạnh |

### Câu hỏi mở
1. Khi hai đại lý báo trùng, ưu tiên tính theo ngày nhận báo hay theo ngày được duyệt? (cần: chị Hạnh)
2. Đại lý lớn có thật sự được ưu tiên hoặc gia hạn không, và nếu có thì ai quyết, theo tiêu chí nào? (cần: chị Hạnh, anh Quang)
3. Ngưỡng chiết khấu phải hỏi Giám đốc Kinh doanh hiện là 8%, 10% hay mức nào khác, và văn bản nào quy định? (cần: anh Quang, chị Hạnh)
4. "Khoảng 3 tháng" có phải 90 ngày kể từ ngày duyệt không, và gia hạn tối đa mấy lần? (cần: chị Hạnh)
5. Quy trình báo bổ sung thông tin dự án (mục §10) hiện làm thế nào? (cần: chị Hạnh)
6. Mã ĐL trong file có tương ứng một-một với mã đại lý trong ERP không, hay cần bảng đối chiếu trước khi import? (cần: chị Hạnh, chị Loan)
7. Tài liệu này do ai viết, lần cuối cập nhật khi nào, và có đang được dùng đúng như mô tả không? (cần: chị Hạnh)
