# Mẫu đặc tả use case đầy đủ (8 phần)

Tham chiếu cho skill `write-use-case-spec`. Sao chép khung này, điền từng ô; ô nào chưa có nguồn thì ghi `[GIẢ ĐỊNH]`, không để trống.

```markdown
## UC-xx <Tên use case: động từ + đối tượng>

### 1. Thông tin chung
| Mục | Nội dung |
|---|---|
| Mã / Tên | UC-xx / <tên> |
| Mô tả | <một câu: actor đạt được gì> |
| Chức năng liên quan | F-xx <tên chức năng trong function tree> |
| Yêu cầu liên quan | R-xx, R-yy |
| Trigger | <sự kiện actor làm để bắt đầu> |
| Mức ưu tiên / Phase | <Phase 1 / Phase 2> |

### 2. Actor
Chính: <actor đạt mục tiêu>
Phụ / hệ thống ngoài: <hệ thống hoặc người tham gia nhưng không phải bên đạt mục tiêu>

### 3. Precondition
- <điều phải đúng trước khi use case bắt đầu>

### 4. Postcondition
- Thành công: <trạng thái dữ liệu và thông báo sau khi xong>
- Thất bại: <trạng thái khi dừng ở một exception; nếu mỗi E một khác thì ghi tại E>

### 5. Main flow
| Bước | Chủ thể | Hành động |
|---|---|---|
| 1 | <actor/hệ thống> | <một hành động> |

### 6. Alternative flows (tối thiểu 2)
**A1 <tên>** (tại bước n) → <quay lại bước m | kết thúc với trạng thái X>
1. <bước xử lý, mỗi bước một chủ thể một hành động>

### 7. Exception flows (tối thiểu 3)
**E1 <tên>** (tại bước n) → <quay lại bước m | kết thúc với trạng thái X>
1. <bước xử lý>

### 8. Business rules và truy vết
| Mã | Nội dung | Áp dụng tại | Nguồn |
|---|---|---|---|
| BR-xx | <rule> | bước n, A/E | <tài liệu, người xác nhận> |

Truy vết: yêu cầu R-xx → UC-xx → bước/luồng → (user story US-xx, AC-xx ở bước sau)

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
```

## Phân biệt alternative và exception
| | Alternative flow | Exception flow |
|---|---|---|
| Bản chất | Lựa chọn hợp lệ khác để vẫn tiến tới mục tiêu hoặc một kết quả nghiệp vụ chấp nhận được | Điều ngăn actor đạt mục tiêu: lỗi, vi phạm rule, hệ thống ngoài hỏng |
| Ví dụ | Lưu nháp, xin ưu đãi thêm, chọn cách giao khác | Hết hàng, quá hạn công nợ, hệ thống ngoài không phản hồi, mất mạng |
| Kết thúc | Thường quay lại main flow hoặc tới một trạng thái chờ hợp lệ | Thông báo cho actor và về trạng thái an toàn |

## Gợi ý tìm exception khi input ít
Dữ liệu không hợp lệ · không đủ tồn/quota · vi phạm business rule · hệ thống ngoài lỗi hoặc quá thời gian chờ · mất kết nối giữa chừng · phiên hết hạn · không đủ quyền · thao tác trùng (gửi hai lần). Mọi exception đề xuất thêm phải gắn `[GIẢ ĐỊNH]` và nêu trong "Câu hỏi mở".

## Quy ước mã (để sơ đồ và user story trích dẫn)
- Bước main flow: số nguyên liên tục. Bước trong luồng: `A1.1`, `E2.1`, hoặc đánh số trong từng luồng.
- Mã A và E duy nhất trong một use case. Không đánh số lại sau khi đã được tham chiếu.
- Điểm rẽ nhánh luôn ghi bằng "tại bước n" của main flow.
