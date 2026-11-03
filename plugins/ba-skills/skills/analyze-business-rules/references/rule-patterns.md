# Tham chiếu: nhận diện, phân loại và đối chiếu rule (analyze-business-rules)

## Tín hiệu có rule trong văn bản
Phải · bắt buộc · không được · cấm · chỉ · chỉ khi · nếu... thì · mỗi · tất cả · tối đa · tối thiểu · dưới · trên · từ... đến · sau... ngày · được duyệt bởi · trừ khi · mặc định · luôn.

## Phân loại Definition và Behaviour
- **Definition:** nói một thuật ngữ nghĩa là gì, gồm những thành phần nào, được tính ra sao. Bỏ rule đi thì nghĩa của thuật ngữ đổi. Ví dụ: "dự án trùng là dự án giống cả ba thuộc tính...", "chiết khấu tính trên giá niêm yết".
- **Behaviour:** ai, khi nào, được hoặc phải hoặc không được làm gì. Bỏ rule đi thì thuật ngữ vẫn nguyên nghĩa nhưng hành vi hệ thống hoặc con người đổi.
- Phép thử nhanh: "Bỏ rule này thì nghĩa của từ đổi, hay chỉ việc được làm đổi?"
- Rule hay lưỡng tính: thời hạn, ngưỡng (có thể là một phần định nghĩa của khái niệm, cũng có thể là ràng buộc hành vi). Chọn một loại, nói lý do trong Ghi chú.

## Kiểu của rule Behaviour
| Kiểu | Dấu hiệu |
|---|---|
| Bắt buộc | "phải", "mỗi... có..." |
| Cấm | "không được", "chưa được", "chỉ được xem..." (giới hạn quyền) |
| Cho phép | "được", "có thể" |
| Điều kiện–hành động | "nếu... thì...", ngưỡng, mức |

## Mức mâu thuẫn
- **Trực tiếp:** hai rule không thể cùng đúng với cùng một tình huống.
- **Gián tiếp (căng thẳng):** cùng đúng chỉ khi thêm một điều kiện ngầm (ví dụ rule chỉ áp cho một vai).
- **Khoảng trống:** có tình huống thật mà không rule nào phủ.
- **Mơ hồ:** có rule nhưng hai người hiểu khác nhau (ví dụ tiêu chí "trùng").

## Danh sách soát khoảng trống ở biên
- Đúng giá trị ngưỡng (có bao gồm không?).
- Hết hạn, quá hạn: tính từ mốc nào, sau đó thì sao?
- Đang chờ xử lý: rule có áp cho trạng thái chờ không?
- Hai sự kiện xảy ra cùng lúc hoặc chạy chồng nhau: thứ tự ưu tiên?
- Rule áp cho vai nào? Vai khác thì sao?
- Rule bị từ chối hoặc hủy giữa chừng: trạng thái sau đó?

## So khớp dữ liệu ("trùng") — ba mức để BA chọn
| Mức | Cách so | Rủi ro |
|---|---|---|
| A. Khớp tuyệt đối | so từng ký tự | bỏ lọt bản ghi chỉ khác hoa/thường, khoảng trắng, dấu |
| B. Chuẩn hóa rồi khớp | bỏ mọi khoảng trắng, hoa/thường và dấu tiếng Việt (kể cả Đ thành D), rồi so tuyệt đối | vẫn bỏ lọt khác biệt do viết tắt hoặc gõ sai; có thể gộp nhầm hai tên khác nhau thật chỉ khác khoảng trắng |
| C. B kèm cờ "nghi trùng" | thêm: khác nhau tối đa một ký tự thì gắn cờ cho người xem, không tự chặn | tăng công duyệt tay, có thể cờ nhầm hai bản ghi khác nhau thật |
Skill chỉ trình bày kết quả của từng mức trên dữ liệu ví dụ; chọn mức nào là quyết định của BA và chủ sở hữu rule.

## Mã rule
- Giữ nguyên mã có trong đầu vào.
- Rule chưa có mã: gán mã tạm theo nhóm, ghi chú "mã tạm `[GIẢ ĐỊNH]`", để BA đổi theo quy ước dự án. Với case Đại Việt Electric, mã chuẩn đã có trong `_shared/case-dai-viet-electric.md` (BR-D, BR-C, BR-P); dùng đúng các mã đó.
- Rule nhiều mức (ví dụ ngưỡng chiết khấu) có thể giữ là một rule, ghi chú "rule bảng quyết định" và kèm bảng quyết định ở mục 2 của đầu ra.
- Mã chỗ thiếu hoặc mâu thuẫn: GAP-nn. Mã cặp thử so khớp: TP-n. Mã mâu thuẫn giữa các rule: X-nn.
