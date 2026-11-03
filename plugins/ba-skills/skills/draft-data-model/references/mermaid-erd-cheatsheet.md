# Mermaid erDiagram: tóm tắt cho mô hình logical

## Ký hiệu cardinality (đọc từ ngoài vào trong, mỗi đầu là "phía đó có bao nhiêu")
| Ký hiệu | Nghĩa |
|---|---|
| `\|\|` | đúng một |
| `\|o` / `o\|` | không hoặc một |
| `}o` / `o{` | không hoặc nhiều |
| `}\|` / `\|{` | một hoặc nhiều |

Dòng quan hệ: `A <trái>--<phải> B : "nhãn"`. Đường `--` là identifying (thực thể con phụ thuộc cha); `..` là non-identifying. Ở mức logical cho nghiệp vụ, dùng `--` cho gọn.

Cách đọc `DAI_LY ||--o{ DON_HANG : "đặt"`: mỗi DON_HANG thuộc đúng một DAI_LY; một DAI_LY có không hoặc nhiều DON_HANG.

Khóa ngoại cho phép rỗng (ví dụ người duyệt chưa có): dùng `|o` ở phía thực thể được trỏ. Ví dụ `NHAN_VIEN |o--o{ DU_AN_BAO`.

## Khối thuộc tính
```
TEN_THUC_THE {
    kieu ten_truong PK "ghi chú tùy chọn"
}
```
- Kiểu logical dùng chung: `string`, `int`, `decimal`, `date`, `datetime`, `boolean`. Không dùng kiểu riêng của nền tảng.
- Khóa: `PK`, `FK`, `UK`. Mỗi thuộc tính ghi một khóa để tránh lỗi parser ở bản cũ.
- Ghi chú đặt trong ngoặc kép, đặt cuối dòng. Dùng ghi chú để nêu nguồn (`ERP`), `[GIẢ ĐỊNH]`, tập giá trị.

## Quy ước đặt tên
- Tên thực thể: IN HOA không dấu, nối bằng `_`, số ít (`DON_HANG`). Tên hiển thị tiếng Việt có dấu ghi ở bảng mô tả.
- Tên trường: chữ thường không dấu, nối bằng `_` (`ngay_giao_mong_muon`).
- Nhãn quan hệ: động từ ngắn, tiếng Việt có dấu, luôn trong ngoặc kép.

## Lỗi thường gặp
| Lỗi | Cách sửa |
|---|---|
| Tên có dấu cách hoặc dấu tiếng Việt | Đổi sang không dấu, nối `_` |
| Nhãn quan hệ không có ngoặc kép | Thêm ngoặc kép |
| Ghi chú có ngoặc kép bên trong | Bỏ ngoặc kép lồng, dùng dấu nháy đơn hoặc bỏ |
| Hai khóa trên một thuộc tính (`PK, FK`) bị lỗi ở bản cũ | Chỉ ghi khóa quan trọng nhất, nêu phần còn lại ở bảng mô tả |
| Quan hệ nhiều-nhiều vẽ thẳng giữa hai thực thể | Tách bằng thực thể trung gian (như dòng đơn giữa đơn hàng và sản phẩm) |
| Thuộc tính tính được (tổng tiền) nằm trong ERD | Bỏ, ghi ở mục trường tính |

## Chuẩn hóa tối thiểu (đủ cho logical)
1. Không nhóm trường lặp (`san_pham_1`, `san_pham_2`): tách thực thể con.
2. Mỗi thuộc tính phụ thuộc vào khóa của chính thực thể đó, không phụ thuộc thuộc tính khác.
3. Không lưu giá trị tính được từ nơi khác; nếu cố ý lưu (chụp giá lúc đặt) thì ghi lý do trong ghi chú.
