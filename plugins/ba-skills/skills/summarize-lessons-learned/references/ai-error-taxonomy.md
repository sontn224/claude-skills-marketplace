# Tham chiếu: phân loại lỗi AI và nối về skill (summarize-lessons-learned)

## Vì sao có phần này
Mỗi lỗi AI lặp lại là dấu hiệu skill chưa chặn được một kiểu sai. Retro là nơi duy nhất mọi lỗi được nói chung một chỗ, nên tổng kết bài học phải đưa lỗi về đúng skill để sửa. Sau khi trainer sửa skill và chấm lại bằng `_checklist/skill-quality.md`, lỗi tương tự không nên xuất hiện ở dự án sau.

## Loại lỗi và mục SKILL.md nên chặn
| Loại lỗi | Dấu hiệu | Mục nên sửa | Mẫu đề xuất |
|---|---|---|---|
| Bịa dữ kiện | Con số, ngưỡng, tên, mã không có trong đầu vào | 5 Tự kiểm, 2 Đầu vào | Nếu skill đích chưa có: thêm câu tự kiểm về nguồn của con số. Nếu đã có: làm cứng thành thao tác đếm được (bảng con số → mã BR, số dòng bằng số con số) và thêm ví dụ sai; thiếu nguồn thì để trống và đưa vào Câu hỏi mở |
| Thiếu nhánh | Chỉ có happy path, thiếu exception, trạng thái, trường hợp biên | 3 Các bước, 5 Tự kiểm | Nếu skill đích chưa có: thêm bước duyệt theo checklist (mỗi lần gọi hệ thống ngoài, mỗi nhập liệu, mỗi quyết định hỏi: lỗi, không phản hồi, từ chối?). Nếu đã có: thêm quy tắc đếm theo bước (bước gọi hệ thống ngoài → exception tương ứng) và ví dụ sai |
| Sai rule | Trái với business rule đã có trong đầu vào | 3 Các bước, 5 Tự kiểm | Thêm bước đối chiếu với BR trước khi trả kết quả |
| Lẫn thuật ngữ | Cùng một khái niệm gọi nhiều tên (ví dụ "khách hàng" và "đại lý") | 2 Đầu vào, 5 Tự kiểm | Yêu cầu glossary là đầu vào; thêm câu tự kiểm về dùng nhất quán |
| Quá tự tin | Không gắn `[GIẢ ĐỊNH]`, trình bày suy đoán như sự thật | 5 Tự kiểm, 6 BA phải verify | Nhắc nhãn `[GIẢ ĐỊNH]`; thêm vào mục 6 chỗ AI hay đoán |
| Sai định dạng | Sai mẫu đầu ra, thiếu cột, thiếu "Câu hỏi mở" | 4 Mẫu đầu ra | Làm mẫu rõ hơn hoặc thêm câu tự kiểm về cấu trúc |
| Không phải lỗi AI | Lỗi quy trình, thiếu thông tin đầu vào, yếu tố bên ngoài | — | Đưa vào hành động quy trình, không sửa skill |

## Bảng tra: loại tài liệu và skill sinh ra nó
| Tài liệu | Skill (slug) |
|---|---|
| Tóm tắt tài liệu nguồn | analyze-source-documents |
| Từ điển thuật ngữ | build-glossary |
| Sơ đồ ý tưởng | build-mind-map |
| Khảo sát | design-survey-and-analyze |
| Kết quả brainstorming | facilitate-brainstorming |
| Kế hoạch workshop | plan-requirements-workshop |
| Câu hỏi phỏng vấn | prepare-stakeholder-interview |
| Từ điển dữ liệu | build-data-dictionary |
| Mô hình dữ liệu | draft-data-model |
| Sequence diagram | draw-sequence-diagram |
| State diagram | draw-state-diagram |
| Màn hình prototype, mockup | generate-prototype-screens |
| Quy trình nghiệp vụ | model-business-process |
| Yêu cầu phi chức năng | write-nfr |
| Use case | write-use-case-spec |
| User story và AC | write-user-story-and-ac |
| Review yêu cầu | pre-review-requirements |
| Phân tích business rule | analyze-business-rules |
| SWOT | draft-swot |
| Rủi ro | identify-risks |
| Benchmark | research-benchmark |
| Tổng kết bài học | summarize-lessons-learned |
| Nguyên nhân gốc | analyze-root-cause |
| Phân tích dữ liệu sử dụng | mine-usage-data |

Một tài liệu do nhiều skill hoặc nhiều lần chạy tạo thì không đoán: ghi các skill ứng viên và đưa vào câu hỏi mở cho trainer.

## Tiêu chí "lặp lại"
- Từ hai lần xuất hiện trở lên, ở các tài liệu khác nhau hoặc các giai đoạn khác nhau; hoặc
- một lần nhưng log các lần retro trước đã có lỗi cùng loại ở cùng skill.
- Một sự cố được nhắc hai lần trong ghi chú không tính là hai lần.

## Mức ưu tiên
- **Cao:** lặp lại ở từ hai skill trở lên hoặc gây làm lại, bug nặng, quyết định sai.
- **Trung bình:** lặp lại ở một skill, bắt được ở review trước khi gây hậu quả.
- **Thấp:** lặp lại nhưng hậu quả nhỏ (trình bày, câu chữ).

## Cách ghi đề xuất sửa
0. Mở SKILL.md của skill đích, đọc mục 1 (Mục đích) và mục 3 (Các bước), 5 (Tự kiểm) trước. Quy tắc đã có thì ghi lại là "đã có" và chỉ đề xuất làm cứng hơn (quy tắc đếm được, ví dụ sai); không đề xuất lặp lại.
1. Nêu skill (slug), mục số mấy của SKILL.md.
2. Viết nội dung thêm hoặc đổi ở mức câu chữ cụ thể, để trainer dán được.
3. Cách kiểm tra lại: chạy lại `examples/input.md`; với lỗi bịa dữ kiện, chạy thêm một lần có chủ ý bỏ dữ kiện đó khỏi đầu vào và kiểm tra AI để trống hoặc hỏi lại thay vì điền.
4. Sau khi sửa: chạy lại 3 lần để chấm "Ổn định", cập nhật bảng chấm.
