# Cú pháp Mermaid stateDiagram-v2 dùng trong BA

Tham chiếu cho skill `draw-state-diagram`.

## Khung cơ bản
```
stateDiagram-v2
    direction LR
    state "Chờ tiếp nhận" as ChoTiepNhan
    state "Đang xử lý" as DangXuLy

    [*] --> ChoTiepNhan : T1 Đại lý gửi yêu cầu
    ChoTiepNhan --> DangXuLy : T2 Kỹ thuật tiếp nhận
    DangXuLy --> [*]
```
- `[*]` là điểm bắt đầu (khi đứng trước mũi tên) hoặc điểm kết thúc (khi đứng sau).
- Id trạng thái chỉ dùng chữ ASCII, không dấu cách (`ChoTiepNhan`). Tên tiếng Việt khai báo bằng `state "Tên" as Id`.
- Nhãn mũi tên: `Nguồn --> Đích : T3 Sự kiện [guard]`. Mã `T` đặt đầu nhãn.

## Nên và không nên trong nhãn
- Nên: ngắn, một dòng; sự kiện là cụm động từ ("Đại lý bổ sung"); guard ngắn ("thiếu ảnh hoặc serial").
- Không dùng `;`, `#`, hoặc xuống dòng trong nhãn. Chi tiết điều kiện dài chuyển sang cột Guard của bảng chuyển.
- Tránh `<`, `>` trong nhãn; viết bằng chữ ("quá 48 giờ").

## Tránh nhầm
| Đừng | Nên |
|---|---|
| Trạng thái là hành động ("Duyệt đơn") | Trạng thái là tình trạng ("Chờ duyệt", "Đã duyệt"); hành động nằm trên mũi tên |
| Một trạng thái cho mỗi bước nhỏ | Gộp bước nhỏ vào "Đang xử lý" cho tới khi nghiệp vụ cần phân biệt |
| Mũi tên không mã | Mỗi mũi tên có `T` và một dòng trong bảng |
| Nhiều mũi tên ra từ một trạng thái mà guard chồng nhau | Guard loại trừ nhau hoặc ghi thứ tự ưu tiên |

## Ma trận chuyển trạng thái (tùy chọn)
Khi có từ 6 trạng thái trở lên, thêm ma trận hàng = trạng thái nguồn, cột = trạng thái đích; ô ghi mã `T`, ô trống là không cho phép, dùng để phát hiện chuyển bị thiếu.

| Từ \ Đến | A | B | Hoàn tất |
|---|---|---|---|
| A | | T2 | |
| B | T3 | | T4 |

## Lỗi hay gặp
- Trạng thái chỉ có mũi tên đi vào mà không có đường tới trạng thái cuối.
- Dùng cùng một tên trạng thái cho hai ý nghĩa khác nhau.
- Quên chuyển do timer (hết hạn, tự động chuyển cấp) vì không có actor nào bấm nút.
