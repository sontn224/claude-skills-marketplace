# Cú pháp Mermaid sequenceDiagram dùng trong BA

Tham chiếu cho skill `draw-sequence-diagram`.

## Khai báo participant
```
sequenceDiagram
    actor DL as Đại lý
    participant CD as Cổng đại lý
```
- `actor` cho người, `participant` cho hệ thống. Id (`DL`, `CD`) chỉ dùng chữ ASCII; tên hiển thị sau `as`.
- Thứ tự khai báo là thứ tự các cột từ trái sang phải.

## Loại mũi tên
| Cú pháp | Ý nghĩa | Dùng cho |
|---|---|---|
| `A->>B: nhãn` | Mũi tên liền, đầu nhọn | Yêu cầu, lời gọi |
| `B-->>A: nhãn` | Mũi tên đứt | Phản hồi, kết quả trả về |
| `A-)B: nhãn` | Mũi tên mở (bất đồng bộ) | Gửi rồi không chờ (email, sự kiện) |
| `A->>A: nhãn` | Self-message | Xử lý nội bộ của một hệ thống |
| `Note over A,B: nội dung` | Ghi chú | Hết thời gian chờ, giả định |

## Khối điều khiển
```
alt E2 Quá hạn công nợ
    ... message ...
else E3 ERP không phản hồi
    ... message ...
else Luồng chính
    ... message ...
end

opt A1 Xin chiết khấu thêm
    ... message ...
end

loop Đến khi đủ tồn kho
    ... message ...
end
```
- `alt` có thể có nhiều `else`. Mỗi khối đều phải có `end`.
- Có thể lồng khối trong khối nhưng nên tránh quá hai cấp để sơ đồ còn đọc được.

## Quy ước nhãn
- Mã bước đặt đầu nhãn: `[b7a] Kiểm tra công nợ`.
- Tên khối `alt` bắt đầu bằng mã luồng trong spec (`E2`, `A1`).
- Không dùng `;` và `#` trong nhãn (Mermaid hiểu là ký tự điều khiển). Tránh dấu `%`, `<`, `>` trong nhãn; viết bằng chữ ("dưới 5%" thành "dưới 5 phần trăm" nếu render lỗi).
- Nhãn ngắn, một dòng; chi tiết dài chuyển sang bảng truy vết.

## Lỗi hay gặp
- Quên `end` làm cả sơ đồ lỗi.
- Id participant có dấu hoặc khoảng trắng.
- Phản hồi không có lời gọi tương ứng (mũi tên `-->>` mồ côi).
- Dùng `autonumber` cùng mã bước `[bN]` gây hai hệ số khác nhau trong một nhãn; chọn một cách (khuyến nghị: chỉ mã bước).
