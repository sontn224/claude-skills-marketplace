---
name: draft-swot
description: Lập bảng SWOT (điểm mạnh, điểm yếu, cơ hội, thách thức) từ tài liệu nghiên cứu và hiện trạng do người dùng cung cấp, mỗi ý ghi nguồn, kèm hành động đề xuất. Dùng khi cần nhìn tổng thể hiện trạng trước khi chọn hướng thay đổi, ví dụ "phân tích SWOT", "đánh giá hiện trạng kênh đại lý", "lập SWOT cho dự án". Không dùng khi cần so sánh các phương án cụ thể theo tiêu chí (dùng research-benchmark), liệt kê rủi ro có điểm số và người phụ trách (dùng identify-risks), tìm nguyên nhân gốc của một vấn đề đã xảy ra (dùng analyze-root-cause) hoặc chỉ cần tóm tắt, trích rule, thuật ngữ từ một tài liệu (dùng analyze-source-documents).
---

# Phân tích SWOT (SWOT Analysis)

## 1. Mục đích
SWOT Analysis giúp nhìn nhanh tình trạng hiện tại của một tổ chức, một kênh hoặc một quy trình: điều gì bên trong đang giúp (Strengths) hoặc cản (Weaknesses), điều gì bên ngoài đang mở đường (Opportunities) hoặc đe dọa (Threats). Kết quả dùng để chọn hướng thay đổi và ưu tiên hành động. Skill này chỉ tổng hợp những gì có trong tài liệu người dùng đưa; không tự bổ sung kiến thức thị trường.

## 2. Đầu vào cần có
- Phạm vi phân tích: toàn công ty, một kênh, hay một quy trình; mốc thời gian (bắt buộc).
- Tài liệu nghiên cứu hoặc mô tả hiện trạng: ghi chú phỏng vấn, mô tả quy trình, số liệu, báo cáo nội bộ (bắt buộc, ít nhất một nguồn).
- Mục tiêu dùng SWOT: để quyết định điều gì (bắt buộc).
- Dữ liệu bên ngoài như thị trường, đối thủ, quy định (tùy chọn). Không có thì ô Opportunities/Threats có thể ít ý.
- Vai nhận hành động, nếu người dùng muốn gán sẵn (tùy chọn).

Thiếu đầu vào bắt buộc nào thì **hỏi lại người dùng trước khi làm**. Không tự bịa để lấp chỗ trống.

## 3. Các bước
1. Chốt phạm vi và mục tiêu dùng SWOT; nếu phạm vi quá rộng so với tài liệu, nói rõ và thu hẹp.
2. Lập bảng nguồn: gán ID S1, S2... cho từng tài liệu người dùng đưa, ghi loại nguồn (tài liệu, ghi chú phỏng vấn, số liệu).
3. Rút từng dữ kiện thành một ý ngắn, mỗi ý trỏ về ít nhất một ID nguồn.
4. Phân loại: Strengths/Weaknesses là yếu tố bên trong, tổ chức kiểm soát được; Opportunities/Threats là yếu tố bên ngoài. Ý hai mặt thì xếp một ô và ghi lý do.
5. Gắn trạng thái cho từng ý: `Có nguồn`, `[GIẢ ĐỊNH]` (AI suy ra, hoặc nguồn tự gắn giả định), `Cần xác minh`. Không có dữ liệu bên ngoài thì **không bịa** Opportunities/Threats; ghi vào "Khoảng trống nguồn".
6. Bỏ ý chung chung, gộp ý trùng.
7. Lập hành động theo ma trận TOWS; mỗi hành động trỏ về ID các ý và có vai phụ trách đề xuất. Loại phải khớp ý nguồn: SO = Strengths + Opportunities; WO = Weaknesses + Opportunities; ST = Strengths + Threats; WT = Weaknesses + Threats. Ý phụ trợ thuộc loại khác ghi riêng là "hỗ trợ", không dùng để xác định loại.
8. Liệt kê khoảng trống nguồn và câu hỏi mở.

## 4. Mẫu đầu ra
```
## SWOT: <phạm vi> (<mốc thời gian>)
Mục tiêu: <quyết định cần hỗ trợ>

### 1. Nguồn đã dùng
| ID | Tài liệu | Loại nguồn | Ghi chú độ tin cậy |

### 2. SWOT
#### Strengths (bên trong)
| ID | Ý | Nguồn | Trạng thái |
#### Weaknesses (bên trong)
| ID | Ý | Nguồn | Trạng thái |
#### Opportunities (bên ngoài)
| ID | Ý | Nguồn | Trạng thái |
#### Threats (bên ngoài)
| ID | Ý | Nguồn | Trạng thái |

### 3. Hành động đề xuất (TOWS)
| ID | Loại | Hành động | Dựa trên | Vai phụ trách đề xuất |

### 4. Khoảng trống nguồn
- <ô nào thiếu dữ liệu, cần loại tài liệu gì>

### Câu hỏi mở
1. <câu hỏi, ghi rõ cần ai trả lời>
```
ID ý dùng STR-1.., WEA-1.., OPP-1.., THR-1.. (ý) và TOWS-1.. (hành động). Ví dụ đầy đủ: `examples/output.md`.

## 5. Tự kiểm trước khi trả kết quả
- [ ] Mọi ý trong bốn ô có cột Nguồn trỏ về một ID có trong bảng nguồn? Không có ID hoặc tài liệu bịa?
- [ ] Ý Strengths/Weaknesses thật sự nằm trong tầm kiểm soát của tổ chức; Opportunities/Threats thật sự bên ngoài?
- [ ] Ý do AI suy ra đã gắn `[GIẢ ĐỊNH]` hoặc `Cần xác minh`; số liệu mà nguồn đã gắn giả định thì giữ nhãn đó?
- [ ] Ô thiếu dữ liệu đã được nêu ở "Khoảng trống nguồn" thay vì lấp bằng ý chung chung?
- [ ] Mỗi hành động TOWS có loại khớp ID nguồn (ví dụ WO phải có ít nhất một WEA và một OPP), có vai phụ trách đề xuất, không thêm việc ngoài phạm vi?
- [ ] Đầu ra kết thúc bằng "Câu hỏi mở", câu hỏi xuất phát từ chỗ thiếu thật của nguồn?

## 6. BA phải verify
- Ranh giới trong/ngoài: AI hay nhét ý nội bộ vào Opportunities/Threats để ô nhìn đầy.
- Số liệu và tỷ lệ: đối chiếu với nguồn gốc; nhãn `[GIẢ ĐỊNH]` kế thừa từ nguồn phải được giữ.
- Ý về thị trường, đối thủ, quy định nghe hợp lý nhưng không truy được về ID nguồn: AI dễ bịa. Gặp thì xóa hoặc yêu cầu tài liệu.
- Ý hai mặt (vừa mạnh vừa yếu) xếp ô nào là quyết định của BA cùng bên nghiệp vụ.
- Hành động chỉ là đề xuất: vai phụ trách, thứ tự ưu tiên và tính khả thi phải được xác nhận.

## 7. An toàn dữ liệu
- Không đưa dữ liệu khách hàng thật vào. Dùng dữ liệu đã ẩn danh.
- Gắn nhãn `[GIẢ ĐỊNH]` cho mọi rule, số liệu, tên riêng không có nguồn trong đầu vào.
- Không đưa thông tin mật của đối thủ hoặc khách hàng (giá, hợp đồng, công nợ) vào SWOT; nguồn có chứa thì ẩn trước.
- SWOT nói về tổ chức, quy trình, năng lực; không đánh giá điểm mạnh/yếu của từng cá nhân. Không đưa nhận xét tính cách stakeholder; nêu ràng buộc quy trình thay thế (ví dụ "họp 1 buổi/tuần").

## 8. Câu hỏi mở
Luôn kết thúc đầu ra bằng mục này:

```
### Câu hỏi mở
1. <câu hỏi còn thiếu, ghi rõ cần ai trả lời>
```
