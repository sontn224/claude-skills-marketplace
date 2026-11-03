# Ký hiệu BPMN và cách vẽ bằng Mermaid flowchart

Tài liệu tham chiếu cho skill `model-business-process`. Mermaid không phải công cụ BPMN đầy đủ nên chỉ dùng tập con dưới đây.

## Bảng ký hiệu

| Phần tử BPMN | Ý nghĩa | Cú pháp Mermaid | Quy ước mã |
|---|---|---|---|
| Lane / Pool | Một actor hoặc hệ thống | `subgraph LA["Tên lane"] ... end` | id `L` + chữ viết tắt |
| Start event | Sự kiện kích hoạt quy trình | `ST(["Mô tả sự kiện"])` | `ST` (nhiều start: `ST1`, `ST2`) |
| Task | Một hoạt động do một lane thực hiện | `P1["Động từ + đối tượng"]` | `P1, P2...` theo thời gian |
| Sub-process | Quy trình con vẽ ở sơ đồ riêng | `SUB1[["QT-1.1 Tên"]]` | `SUB1, SUB2...` |
| Exclusive gateway | Rẽ nhánh, chỉ một nhánh được chọn | `GW1{"Câu hỏi?"}` | `GW1, GW2...` |
| End event | Kết quả cuối của một đường đi | `EN1(["Kết quả"])` | `EN1, EN2...` |
| Sequence flow | Thứ tự thực hiện | `P1 --> P2` | |
| Flow có điều kiện | Nhánh ra khỏi gateway | `GW1 -- "Có" --> P2` | nhãn là điều kiện |
| Message flow | Bàn giao giữa hai lane | cùng cú pháp mũi tên, khai báo ngoài `subgraph` | |

Không có trong Mermaid flowchart: parallel gateway chuẩn, timer event, data object. Khi cần, mô tả bằng nhãn node (ví dụ "Hết 48 giờ chưa phản hồi") và ghi chú trong bảng bước.

## Quy tắc đặt tên
- Task: động từ + đối tượng, không quá 10 từ ("Tạo đơn hàng", không phải "Đơn hàng").
- Gateway: câu hỏi kết thúc bằng dấu hỏi; nhãn nhánh là giá trị của điều kiện ("Có", "Dưới 5%").
- Id node chỉ dùng chữ ASCII và số; tiếng Việt chỉ nằm trong nhãn đặt trong dấu ngoặc kép.
- Khi dùng `[GIẢ ĐỊNH]` trong sơ đồ, đặt cuối nhãn node hoặc nhãn nhánh.

## Lỗi cú pháp hay gặp
- Nhãn chứa `;`, `#`, hoặc dấu ngoặc mà không đặt trong dấu ngoặc kép.
- Tên node trùng id với từ khóa Mermaid (`end`, `graph`, `subgraph`).
- Khai báo mũi tên chéo lane bên trong `subgraph` làm node bị kéo sang lane sai.
- Nhánh gateway hở: chỉ có "Có" mà thiếu "Không".

## Khi nào tách quy trình con
Sơ đồ quá khoảng 20 nút, hoặc một nhóm hoạt động tự thành một quy trình riêng (ví dụ "Duyệt chiết khấu"). Giữ một node `SUB` ở sơ đồ cha, nối các nhánh ra bằng nhãn kết quả của quy trình con, và vẽ riêng sơ đồ con với nút kết thúc ghi rõ "Về QT-1 tại <mã nút>". Mã `P`, `GW`, `EN` đánh liên tục xuyên các sơ đồ.
