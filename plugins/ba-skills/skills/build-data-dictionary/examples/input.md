# Đầu vào mẫu: build-data-dictionary (case Đại Việt Electric)

## Yêu cầu của người dùng
Lập data dictionary cho các trường của Đơn hàng (DON_HANG) và Dòng đơn (DONG_DON) trong ERD bên dưới. Nhớ giá và tồn kho có nguồn là ERP, không ai sửa trên cổng.

## ERD (đầu ra của skill draft-data-model, dán nguyên)
```mermaid
erDiagram
    NHAN_VIEN ||--o{ DAI_LY : "phụ trách"
    DAI_LY ||--o{ DU_AN_BAO : "báo"
    DAI_LY ||--o{ DON_HANG : "đặt"
    DON_HANG ||--o{ DONG_DON : "gồm"
    SAN_PHAM ||--o{ DONG_DON : "được đặt trong"
    DON_HANG ||--o{ PHE_DUYET_CK : "xin duyệt"
    NHAN_VIEN |o--o{ PHE_DUYET_CK : "duyệt"
    NHAN_VIEN |o--o{ DU_AN_BAO : "duyệt bảo hộ"

    NHAN_VIEN {
        string ma_nhan_vien PK "định danh từ SSO nội bộ"
        string ho_ten
        string vai_tro "Sales khu vực, TP Quản lý kênh, GĐ Kinh doanh, Kế toán, Sales admin [GIẢ ĐỊNH một vai mỗi người]"
    }
    DAI_LY {
        string ma_dai_ly PK
        string ma_dai_ly_erp UK "ERP, khóa nối và lọc trùng khi import R8"
        string ten_dai_ly
        string tinh_thanh
        string khu_vuc "phân quyền theo vùng (BR-P1), xem R9"
        string hang_dai_ly "quyết định số ngày trả chậm [GIẢ ĐỊNH]"
        string trang_thai "hoạt động, ngừng [GIẢ ĐỊNH]"
        string email_lien_he "nhận email xác nhận đơn"
        string so_dien_thoai
        string ma_nhan_vien_phu_trach FK
    }
    DU_AN_BAO {
        string ma_du_an PK
        string ma_dai_ly FK
        string ten_du_an "so trùng 1/3 (BR-D1)"
        string chu_dau_tu "so trùng 2/3 (BR-D1)"
        string tinh_thanh "so trùng 3/3 (BR-D1)"
        string trang_thai "Chờ duyệt, Đã duyệt (bảo hộ), Bị trùng [GIẢ ĐỊNH tập giá trị]"
        datetime ngay_bao
        string ma_nhan_vien_duyet FK "rỗng đến khi duyệt (BR-D2)"
        datetime ngay_duyet "mốc tính 90 ngày bảo hộ (BR-D3)"
    }
    DON_HANG {
        string ma_don PK
        string ma_dai_ly FK
        string ma_don_erp UK "ERP, rỗng đến khi ghi vào ERP"
        string trang_thai "Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận"
        decimal ty_le_chiet_khau "phần trăm, áp cả đơn, tính trên giá niêm yết (BR-C3)"
        string dia_chi_giao
        date ngay_giao_mong_muon
        date ngay_giao_du_kien "ERP [GIẢ ĐỊNH ERP cung cấp]"
        datetime ngay_tao
        datetime ngay_gui "rỗng đến khi gửi lần đầu"
    }
    DONG_DON {
        string ma_dong_don PK
        string ma_don FK
        string ma_san_pham FK
        int so_luong
        decimal don_gia_niem_yet "ERP, chụp lúc thêm dòng, không sửa (BR-C2)"
    }
    SAN_PHAM {
        string ma_san_pham PK "mã trong ERP"
        string ten_san_pham
        string nhom_san_pham "Tủ điện, Thiết bị đóng cắt, Cáp điện"
        string don_vi_tinh "[GIẢ ĐỊNH]"
        decimal gia_niem_yet "ERP, chỉ đọc (BR-C2)"
        int ton_kho "ERP, chỉ đọc (BR-C2)"
    }
    PHE_DUYET_CK {
        string ma_phe_duyet PK
        string ma_don FK
        decimal ty_le_xin "phần trăm đại lý xin"
        string ly_do "bắt buộc mỗi lần xin (BR-C4)"
        string cap_duyet "TP Quản lý kênh hoặc GĐ Kinh doanh theo BR-C1, lưu theo ngưỡng lúc xin"
        string ma_nhan_vien_duyet FK "rỗng khi chưa duyệt"
        string ket_qua "Chờ, Duyệt, Từ chối [GIẢ ĐỊNH]"
        datetime thoi_diem_gui
        datetime thoi_diem_duyet "rỗng khi chưa duyệt"
    }
```

## Dữ liệu mẫu (bịa, đã ẩn danh `[GIẢ ĐỊNH]`)
DON_HANG:

| ma_don | ma_dai_ly | ma_don_erp | trang_thai | ty_le_chiet_khau | dia_chi_giao | ngay_giao_mong_muon | ngay_tao | ngay_gui |
|---|---|---|---|---|---|---|---|---|
| DH-2026-000101 | DL-0007 | ERP-884201 | Đã xác nhận | 3,00 | Kho đại lý (ẩn danh), Đà Nẵng | 2026-11-20 | 2026-11-03T09:30:00+07:00 | 2026-11-03T09:41:00+07:00 |
| DH-2026-000102 | DL-0012 | (rỗng) | Chờ duyệt chiết khấu | 8,50 | Công trình A (ẩn danh), Hà Nội | 2026-11-25 | 2026-11-03T10:05:00+07:00 | 2026-11-03T10:20:00+07:00 |

DONG_DON:

| ma_dong_don | ma_don | ma_san_pham | so_luong | don_gia_niem_yet |
|---|---|---|---|---|
| DD-00000201 | DH-2026-000101 | SP-0001 | 4 | 1.250.000 |
| DD-00000202 | DH-2026-000102 | SP-0002 | 10 | 380.000 |

## Quy tắc và nguồn đã biết
- BR-C2 (R6): giá niêm yết và tồn kho lấy từ ERP; trên cổng không ai sửa.
- BR-C1: chiết khấu dưới 5%: đại lý tự áp. Từ 5% đến 10%: TP Quản lý kênh duyệt. Trên 10%: Giám đốc Kinh doanh duyệt `[GIẢ ĐỊNH]`. Quy ước đầu mút `[GIẢ ĐỊNH]`: đúng 5% và đúng 10% thuộc bậc 5%–10%; chiết khấu chuẩn của đại lý mặc định 0%.
- BR-C3: chiết khấu tính trên giá niêm yết, áp cho cả đơn.
- BR-C6: đơn chưa duyệt chiết khấu thì chưa ghi vào ERP.
- BR-C7 (R11): đại lý quá hạn công nợ thì đơn giữ lại, Kế toán được thông báo.
- UC-01: trạng thái đơn gồm Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận. Ghi vào ERP thì có mã đơn. Bước 7 gồm 7a kiểm tra công nợ trên ERP và 7b ghi đơn vào ERP. Không đủ tồn kho thì không thêm được dòng (E1). E2 (quá hạn công nợ, bước 7a) → Chờ kế toán xử lý. E3 (BA đề xuất `[GIẢ ĐỊNH]`, ERP không phản hồi ở bước 7, tại 7a hoặc 7b) và E4 (mất kết nối khi gửi, bước 6) → Nháp.
- Tài liệu kỹ thuật ERP chưa có: định dạng mã ERP, mã sản phẩm, độ dài chưa biết.
