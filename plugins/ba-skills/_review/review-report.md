# Báo cáo review chéo ba-skills (24 skill)

Người review độc lập. Không sửa file skill, không chạy git. Báo cáo được ghi theo từng phần, nối thêm dần.

## Tóm tắt điều hành

- **Kết quả đo được:** 24/24 skill đúng tên, đủ frontmatter, đủ 8 mục đúng thứ tự, ≤103 dòng, có input/output, output kết thúc bằng "Câu hỏi mở"; 14/14 khối Mermaid qua `mermaid.parse`; không có SĐT, email, URL, tên người thật; số liệu mine-usage-data tính lại khớp 100%.
- **Lỗi:** 1 Cao, 13 Vừa, 21 Thấp (mục 2). Lỗi Cao: mã luồng **E3** lệch giữa write-use-case-spec và các tài liệu trích dẫn (B-01). Lỗi chủ yếu nằm ở ví dụ, không ở SKILL.md. Không có skill nào được ghi "Đạt" hoàn toàn vì tiêu chí Ổn định chưa kiểm được; 11/24 skill được ghi "Đạt sơ bộ" (không có lỗi Vừa trở lên ở bốn tiêu chí kiểm được) hoặc "Chưa đạt" cho 13/24 (xem 1C).
- **Chuỗi nối tiếp:** Interviews → Glossary khớp một phần; Glossary → Use Case khớp một phần; Use Case → Story/AC lệch ở E3; Use Case → Sequence khớp mã nhưng lệch nghĩa ở bước 7 và E3; State chưa thử trên đơn hàng; Data model → Data dictionary khớp hoàn toàn (ERD giống từng ký tự).
- **Nhất quán:** 8 mục và mục 7 nhất quán; "Câu hỏi mở" có 5 kiểu viết người trả lời; nhãn trạng thái nguồn lệch (Có nguồn rõ / Có nguồn; Cần xác nhận / Cần xác minh); mã định danh va chạm ở G, S, T (mục 3.4); rule đặt hàng và chiết khấu cần mã BR-C1…C7 chính thức (mục 3.3).
- **Chi tiết tự thêm của subagent A:** khuyến nghị giữ nhưng gắn nhãn `[GIẢ ĐỊNH]` (mục 7).
- Mã lỗi trong báo cáo (A-01, B-01…) = chữ subagent gốc + số, chỉ dùng trong báo cáo này, không liên quan mã F1–F9 của case.

## 0. Phương pháp và kết quả đo bằng script

Script (Python + Node, ở scratchpad) chạy trên cả 24 thư mục skill.

| Kiểm tra | Kết quả đo được |
|---|---|
| `name` khớp slug thư mục | 24/24 khớp |
| Frontmatter có name + description | 24/24 |
| Description có "Dùng khi" và "Không dùng khi" | 24/24 |
| Description có ≥2 cụm kích hoạt tiếng Việt trong ngoặc kép | 24/24 (write-nfr có 6 cụm vì trích thêm "nhanh", "bảo mật", "không sập") |
| Đúng 8 mục `##` đúng tên, đúng thứ tự (bỏ qua dòng `##` trong khối code) | 24/24 |
| Số dòng SKILL.md | 75–103 dòng, không skill nào vượt 150 (lớn nhất: draft-data-model 103) |
| Có `examples/input.md` và `examples/output.md` | 24/24 |
| `output.md` kết thúc bằng mục "Câu hỏi mở" | 24/24 |
| Mermaid | 14 khối (7 trong SKILL.md, 7 trong output.md) của build-mind-map, draft-data-model, draw-sequence-diagram, draw-state-diagram, generate-prototype-screens, model-business-process, analyze-root-cause. Cài được `mermaid` + `jsdom`, gọi `mermaid.parse`: 14/14 hợp lệ. Đã thử 2 đoạn sai cú pháp: parser từ chối, nên phép kiểm có hiệu lực. Lưu ý: `parse` chỉ kiểm cú pháp, không kiểm hiển thị (chưa render SVG). |
| Slug trong mục "Không dùng khi" và toàn bộ file .md | Mọi slug dạng `động-từ-danh-từ` đều tồn tại trong repo. Chỉ có 1 chỗ trỏ chung chung: `build-mind-map` ("dùng skill vẽ flow"). Một số skill nêu tình huống loại trừ nhưng không trỏ skill nào (xem mục 2). |
| Dữ liệu thật | Quét regex SĐT, email, URL: không có. Tên người chỉ là nhân vật của case. Output `summarize-lessons-learned` không còn tên người (đã grep). |
| ERD draft-data-model/output.md so với build-data-dictionary/input.md | Giống hệt từng ký tự. |
| mine-usage-data | Tính lại bằng Python từ bảng 17 dòng: mọi số khớp (xem 1.3). |

Tiêu chí 4 (Ổn định) **chưa kiểm được** cho cả 24 skill: không thể chạy model thật 3 lần. Chỉ đánh giá rủi ro dao động từ độ mơ hồ của SKILL.md.

---

## 1A. Tiêu chí 1: Kích hoạt (6 prompt mỗi skill, đối chiếu description của cả 24 skill)

Lưu ý phương pháp: đây là dự đoán từ việc đọc description, không phải chạy router thật. "Nên" = prompt phải chọn skill này. "Không nên" = prompt đáng lẽ thuộc skill ghi sau dấu `→`. Nhãn **rủi ro** = prompt dễ bị skill khác "cướp".

| Skill | 3 prompt NÊN | 3 prompt KHÔNG NÊN (→ skill đúng) | Đoán kết quả / rủi ro |
|---|---|---|---|
| analyze-source-documents | "Phân tích file hướng dẫn duyệt dự án này" / "Trích rule từ quy trình trong tài liệu nội bộ" / "Đọc hợp đồng mẫu đã ẩn danh, liệt kê chỗ mâu thuẫn" | "Soạn câu hỏi hỏi chị Hạnh" → prepare-stakeholder-interview / "Lập bảng thuật ngữ từ 3 tài liệu" → build-glossary / "So sánh 2 báo giá" → research-benchmark | 6/6 theo chữ. **Rủi ro vừa:** prompt không nên số 2 và 3 dễ bị cướp (cặp C1, C3). |
| build-glossary | "Lập bảng thuật ngữ từ biên bản này" / "Chốt định nghĩa 'bảo hộ' và 'trùng'" / "Làm glossary trước khi viết use case" | "Trích rule từ tài liệu" → analyze-source-documents / "Vẽ cây ý phạm vi" → build-mind-map / "Chưa có biên bản, cần hỏi trước" → prepare-stakeholder-interview | 6/6 theo chữ. **Rủi ro vừa-cao** với analyze-source-documents (output của skill kia cũng có bảng Thuật ngữ). |
| build-mind-map | "Vẽ mind map phạm vi dự án" / "Tóm tắt ghi chú kickoff thành sơ đồ cây" / "Gom ghi chú họp thành cây ý" | "Vẽ swimlane quy trình đặt hàng" → model-business-process / "Cho thêm ý tưởng tăng tỉ lệ đơn qua cổng" → facilitate-brainstorming / "Định nghĩa các từ này" → build-glossary | Prompt nên số 2, 3 trùng chữ "tóm tắt", "gom" với skill khác (C5). Prompt không nên số 1: description chỉ ghi "dùng skill vẽ flow", không có slug: **lỗi trỏ chung chung**. |
| design-survey-and-analyze | "Thiết kế khảo sát cho 200 đại lý" / "Soạn bảng hỏi về việc dùng điện thoại" / "Gom 40 câu trả lời mở thành chủ đề" | "Soạn câu hỏi phỏng vấn chị Hạnh" → prepare-stakeholder-interview / "Lên agenda workshop" → plan-requirements-workshop / "Brainstorm ý tưởng" → facilitate-brainstorming | 6/6. **Rủi ro thấp-vừa:** "soạn câu hỏi cho 5 đại lý" mơ hồ giữa survey và interview (hai bên có trỏ qua lại, tốt). |
| facilitate-brainstorming | "Brainstorm cách đưa đơn sang cổng" / "Gom nhóm và chấm điểm 10 ý này" / "Mở rộng danh sách ý của team" | "Chốt rule báo dự án với các bên" → plan-requirements-workshop / "Thu ý kiến 200 đại lý" → design-survey-and-analyze / "Vẽ cây ý" → build-mind-map | 6/6 theo chữ. **Rủi ro vừa:** "gom nhóm" trùng build-mind-map và summarize-lessons-learned (C5). |
| plan-requirements-workshop | "Lên kế hoạch workshop gỡ R9 với BR-D5" / "Soạn agenda 2 giờ" / "Làm mẫu ghi quyết định" | "Hỏi riêng chị Hạnh" → prepare-stakeholder-interview / "Sinh ý tưởng" → facilitate-brainstorming / "Tổng hợp retro sprint" → summarize-lessons-learned | 6/6. **Rủi ro thấp-vừa:** "mẫu ghi quyết định cuộc họp" có thể bị summarize-lessons-learned hút. |
| prepare-stakeholder-interview | "Soạn câu hỏi phỏng vấn chị Loan" / "Chuẩn bị buổi gặp anh Kiên 30 phút" / "Tóm tắt ghi chú sau phỏng vấn thành biên bản" | "Khảo sát 200 đại lý" → design-survey-and-analyze / "Họp 5 người chốt rule" → plan-requirements-workshop / "Chốt thuật ngữ từ biên bản" → build-glossary | Prompt nên số 3 ("tóm tắt biên bản") dễ bị analyze-source-documents hoặc build-glossary cướp (C1). |
| model-business-process | "Vẽ quy trình đặt hàng To-be" / "Vẽ swimlane cho quy trình duyệt dự án" / "Mô hình hóa quy trình As-is" | "Vẽ sequence diagram cho UC-01" → draw-sequence-diagram / "Vòng đời yêu cầu bảo hành" → draw-state-diagram / "Viết use case" → write-use-case-spec | 6/6 trong repo. **Rủi ro ngoài repo:** skill hệ thống `anthropic-skills:ba-flow-diagram` có cụm kích hoạt gần trùng ("vẽ quy trình", "vẽ luồng", "swimlane"); không kiểm được ai thắng (C10). |
| write-use-case-spec | "Viết use case đặt hàng" / "Viết main flow và exception cho UC-02" / "Đặc tả use case đầy đủ 8 phần" | "Viết user story" → write-user-story-and-ac / "Vẽ sequence" → draw-sequence-diagram / "Tách rule từ chính sách" → analyze-business-rules | 6/6 theo chữ. **Rủi ro thấp-vừa:** không trỏ analyze-business-rules (C6). |
| write-user-story-and-ac | "Viết user story cho UC-01" / "Viết acceptance criteria Given/When/Then" / "Tách story từ use case" | "Hiệu năng cổng dưới 3 giây" → write-nfr / "Mô tả màn hình tạo đơn" → generate-prototype-screens / "Chưa có use case" → write-use-case-spec | 6/6 trong repo. **Rủi ro ngoài repo:** `anthropic-skills:sf-functional-design-writer` kích hoạt trên "user story", "acceptance criteria" (C10). |
| draw-sequence-diagram | "Vẽ sequence diagram cho UC-01" / "Luồng gọi giữa cổng và ERP" / "Sơ đồ tuần tự đặt hàng" | "Vẽ quy trình nhiều bộ phận" → model-business-process / "Vòng đời trạng thái đơn" → draw-state-diagram / "Chưa có use case" → write-use-case-spec | **Rủi ro vừa:** "vẽ sơ đồ cho UC-01" (không nói loại) có thể rơi vào model-business-process (C8). |
| draw-state-diagram | "Vẽ state diagram đơn hàng" / "Bảng chuyển trạng thái yêu cầu bảo hành" / "Vòng đời trạng thái dự án đã báo" | "Thứ tự gọi ERP" → draw-sequence-diagram / "Quy trình duyệt nhiều actor" → model-business-process / "Thiết kế bảng dữ liệu" → draft-data-model | 6/6. Rủi ro thấp. |
| generate-prototype-screens | "Dựng prototype tạo đơn" / "Mô tả màn hình cho US-01" / "Vẽ wireframe cho story này" | "Chọn màu và font" → designer (ngoài repo) / "Vẽ luồng nghiệp vụ" → model-business-process / "Chưa có story" → write-user-story-and-ac | **Rủi ro ngoài repo:** `anthropic-skills:designpro`, `design-pro` cũng nhận "wireframe", "mockup", "màn hình" (C10). |
| draft-data-model | "Vẽ ERD cho báo dự án và đặt hàng" / "Xác định thực thể và quan hệ" / "Dựng mô hình dữ liệu logical" | "Định nghĩa từng trường" → build-data-dictionary / "Danh sách thuật ngữ" → build-glossary / "Thiết kế object Salesforce" → (không có skill đích; description loại trừ nhưng không trỏ) | 6/6. |
| build-data-dictionary | "Lập data dictionary cho DON_HANG" / "Định nghĩa các trường" / "Mô tả field của đơn hàng" | "Vẽ ERD" → draft-data-model / "Thuật ngữ nghiệp vụ" → build-glossary / "Phân tích luật chiết khấu" → analyze-business-rules | **Rủi ro thấp:** "mô tả đơn hàng" trần có thể bị glossary hút. Trỏ đúng 3 skill. |
| write-nfr | "Biến 'chạy nhanh' thành con số" / "Viết NFR cho R12" / "Viết yêu cầu phi chức năng về bảo mật" | "Viết AC cho đặt hàng" → write-user-story-and-ac / "Rule chiết khấu" → analyze-business-rules / "Review R1–R12" → pre-review-requirements | 6/6 theo chữ. Ba từ khóa mơ hồ trong ngoặc kép ("nhanh", "bảo mật", "không sập") tăng recall nhưng có thể kéo cả câu hỏi về phân quyền hoặc rủi ro. Không trỏ pre-review-requirements (C7). |
| analyze-business-rules | "Phân tích business rule báo dự án" / "Tách rule từ chính sách chiết khấu" / "Kiểm tra rule có mâu thuẫn không" | "Review cả tài liệu R1–R12" → pre-review-requirements / "Chuẩn hóa thuật ngữ" → build-glossary / "Viết use case từ rule" → write-use-case-spec | **Rủi ro vừa-cao** với pre-review-requirements ("kiểm tra mâu thuẫn") và write-use-case-spec (C6, C7). |
| pre-review-requirements | "Review yêu cầu R1–R12" / "Rà soát tài liệu yêu cầu trước họp" / "Kiểm tra chất lượng spec" | "Viết lại yêu cầu cho rõ" → write-user-story-and-ac / "Chỉ soát business rule" → analyze-business-rules / "Chuyển 'nhanh' thành số" → write-nfr | **Rủi ro vừa** với analyze-business-rules và write-nfr (C7). |
| draft-swot | "Phân tích SWOT kênh đại lý" / "Đánh giá hiện trạng quy trình đặt hàng" / "Lập SWOT cho dự án" | "So sánh Salesforce với web" → research-benchmark / "Rủi ro có điểm số" → identify-risks / "Vì sao đơn chậm" → analyze-root-cause | 6/6. Rủi ro thấp: "đánh giá hiện trạng" cũng khớp analyze-source-documents. |
| identify-risks | "Lập risk register Phase 1" / "Nhận diện rủi ro khi nhận Change Request" / "Đánh giá rủi ro nền tảng" | "Vì sao đơn bị giữ 3 ngày" → analyze-root-cause / "Điểm mạnh yếu kênh" → draft-swot / "Bài học sprint" → summarize-lessons-learned | 6/6. **Rủi ro vừa** khi prompt "phân tích vấn đề X" không nói đã xảy ra hay chưa (C4). |
| research-benchmark | "So sánh web tùy biến và Salesforce" / "Benchmark nền tảng" / "Phân tích thị trường đối thủ" | "SWOT kênh đại lý" → draft-swot / "Rủi ro phương án đã chọn" → identify-risks / "Đọc tài liệu sản phẩm để rút yêu cầu" → analyze-source-documents | **Rủi ro vừa:** prompt không nên số 3 dễ bị cướp ngược vì analyze-source-documents không trỏ lại (C3). |
| summarize-lessons-learned | "Tổng kết bài học Sprint 1" / "Tổng hợp retro" / "Lessons learned sau phase" | "Nguyên nhân gốc bug gửi 2 lần" → analyze-root-cause / "Rủi ro phase tới" → identify-risks / "Biên bản họp thường" → (không có skill; không trỏ) | 6/6. Cặp C5: "gom ghi chú" trùng build-mind-map. |
| analyze-root-cause | "Tìm nguyên nhân gốc đơn bị giữ" / "Phân tích 5 Whys" / "Vẽ xương cá cho sự cố" | "Tỷ lệ đơn qua cổng là bao nhiêu" → mine-usage-data / "Rủi ro chưa xảy ra" → identify-risks / "Hỏi người liên quan" → prepare-stakeholder-interview | **Rủi ro vừa** với mine-usage-data khi prompt là "phân tích đơn hàng bị giữ" (C4). |
| mine-usage-data | "Khai thác dữ liệu sử dụng sau go-live" / "Viết SQL phân tích đơn hàng" / "Đối chiếu số trước khi kết luận" | "Vì sao đơn chậm" → analyze-root-cause / "Hỏi ý kiến đại lý" → design-survey-and-analyze / "Dữ liệu còn tên thật" → (bị từ chối, không trỏ) | 6/6. Rủi ro vừa như trên (C4). |

**Kết luận tiêu chí 1:** theo chữ, cả 24 description có đủ "làm gì", "khi nào dùng", "khi nào không dùng" và ≥3 cụm tiếng Việt. Không ghi "Đạt" vì chưa chạy router thật. Số skill có ít nhất một prompt dễ bị cướp: 14/24 (build-glossary, build-mind-map, facilitate-brainstorming, prepare-stakeholder-interview, analyze-source-documents, research-benchmark, write-use-case-spec, analyze-business-rules, pre-review-requirements, write-nfr, identify-risks, analyze-root-cause, mine-usage-data, draw-sequence-diagram).

## 1B. Các cặp description dễ lẫn nhau

| # | Cặp | Bằng chứng | Rủi ro | Đề xuất sửa description |
|---|---|---|---|---|
| C1 | analyze-source-documents ↔ build-glossary ↔ prepare-stakeholder-interview | analyze-source-documents trích "tóm tắt, rule, thuật ngữ"; build-glossary nhận "tài liệu hoặc biên bản" và trigger "làm glossary từ biên bản"; prepare-stakeholder-interview có trigger "tóm tắt biên bản phỏng vấn". Ba skill cùng nhận "biên bản/tài liệu + thuật ngữ". Output analyze-source-documents cũng có bảng "Thuật ngữ". | Cao | analyze-source-documents: thêm "nguồn là tài liệu viết sẵn, không phải biên bản phỏng vấn". build-glossary: đổi thành "đã có biên bản hoặc ghi chú từ nhiều nguồn, cần chốt tên chuẩn". prepare-stakeholder-interview: đổi trigger thành "điền khung biên bản từ ghi chú thô" để không giống "tóm tắt". |
| C2 | plan-requirements-workshop ↔ facilitate-brainstorming | Trỏ qua lại đủ; khác nhau (chốt quyết định vs sinh ý) rõ. | Thấp | Giữ. |
| C3 | research-benchmark ↔ analyze-source-documents | research-benchmark trỏ analyze-source-documents, nhưng analyze-source-documents **không** trỏ lại (chỉ trỏ prepare-stakeholder-interview, build-glossary, build-mind-map). | Vừa | analyze-source-documents thêm "Không dùng khi cần so sánh nhiều đối tượng theo tiêu chí (dùng research-benchmark)". |
| C4 | identify-risks ↔ analyze-root-cause ↔ mine-usage-data | identify-risks ↔ analyze-root-cause trỏ qua lại; analyze-root-cause ↔ mine-usage-data trỏ qua lại. Nhưng "phân tích đơn hàng bị giữ lâu" khớp trigger "viết SQL phân tích đơn hàng" lẫn "tìm nguyên nhân gốc"; phân biệt nằm ở chữ "vì sao", không ở từ khóa. | Vừa | mine-usage-data đổi trigger thành "viết SQL đo chỉ số đơn hàng so với mục tiêu"; analyze-root-cause thêm "Dùng khi đã biết chỉ số xấu và hỏi vì sao". |
| C5 | build-mind-map ↔ facilitate-brainstorming ↔ summarize-lessons-learned ↔ prepare-stakeholder-interview | Cùng chữ "gom", "tóm tắt", "ghi chú": mind-map "gom ghi chú họp", brainstorming "gom nhóm", lessons "gom ghi chú retro", interview "tóm tắt biên bản". | Vừa | Mỗi description nêu loại ghi chú riêng: kickoff/spec, ý tưởng của team, retro, phỏng vấn. |
| C6 | analyze-business-rules ↔ write-use-case-spec | analyze-business-rules trỏ write-use-case-spec; chiều ngược lại không có. Use case spec có mục 8 "Business rules và truy vết" nên "viết rule cho đặt hàng" vào được cả hai. | Vừa | write-use-case-spec thêm "Không dùng khi chỉ cần tách và chuẩn hóa rule (dùng analyze-business-rules)". |
| C7 | pre-review-requirements ↔ write-nfr ↔ analyze-business-rules | "Kiểm tra R12 có đo được không" khớp cả pre-review (tiêu chí Kiểm chứng được) lẫn write-nfr. "Kiểm tra rule có mâu thuẫn" là trigger của analyze-business-rules nhưng cũng là tiêu chí Nhất quán của pre-review. pre-review trỏ đủ hai skill kia; write-nfr không trỏ pre-review. | Vừa | write-nfr thêm "Không dùng khi cần soát cả tài liệu yêu cầu (dùng pre-review-requirements)". pre-review đổi trigger "kiểm tra chất lượng spec" thành "lọc lỗi trước buổi review". |
| C8 | model-business-process ↔ draw-sequence-diagram ↔ draw-state-diagram | Trỏ qua lại đủ và rõ. Prompt "vẽ sơ đồ cho UC-01" không nói loại. | Thấp-Vừa | Mục 2 của ba skill thêm "người dùng chỉ nói 'vẽ sơ đồ' thì hỏi lại loại sơ đồ". |
| C9 | write-user-story-and-ac ↔ write-nfr ↔ generate-prototype-screens | Trỏ đủ và đúng chiều. | Thấp | Giữ. |
| C10 | Ngoài repo | Skill hệ thống `ba-flow-diagram`, `sf-functional-design-writer`, `designpro`/`design-pro`, `design:user-research`, `design:research-synthesis` trùng cụm kích hoạt với model-business-process, write-user-story-and-ac, generate-prototype-screens, prepare-stakeholder-interview, design-survey-and-analyze. | Chưa đo được | Trainer quyết ưu tiên; nếu ưu tiên repo, thêm cụm đặc trưng ("theo mẫu 8 mục ba-skills") vào description. |

**Mục "Không dùng khi" trỏ slug:** 23/24 trỏ bằng slug có thật. Ngoại lệ chung chung: build-mind-map ("dùng skill vẽ flow", SKILL.md dòng 3; nên là model-business-process). Có nêu tình huống loại trừ nhưng không trỏ skill: draft-data-model ("thiết kế bảng/object cho nền tảng cụ thể"), pre-review-requirements ("thay buổi review có stakeholder"), summarize-lessons-learned ("biên bản họp thông thường"), generate-prototype-screens ("chuyển cho designer"), mine-usage-data ("dữ liệu chưa ẩn danh"). Chấp nhận được vì không có skill đích trong repo, nhưng nên ghi rõ "ngoài repo".

---

## 1C. Bảng chấm 24 skill theo 5 tiêu chí

Quy ước cột:
- **Kích hoạt**: kết quả theo chữ (mục 1A/1B), chưa chạy router thật.
- **Format**: kết quả script (8 mục, tên, thứ tự, ≤150 dòng, có input/output, kết thúc Câu hỏi mở, Mermaid parse) cộng lỗi mẫu mục 4 tìm được khi đọc.
- **Nội dung**: kết quả "chạy tay" SKILL.md lên input rồi so với output, và đối chiếu case.
- **Ổn định**: luôn "Chưa kiểm được", kèm rủi ro dao động.
- **Dữ liệu**: quét regex SĐT/email/URL, tên người, và đọc mục 7 (cả 24 skill đều có mục 7 chứa cả "ẩn danh" lẫn `[GIẢ ĐỊNH]`).
- **Kết luận**: "Chưa đạt" khi còn lỗi Cao/Vừa. "Đạt sơ bộ" chỉ nghĩa là bốn tiêu chí kiểm được đều không thấy lỗi Vừa trở lên; **không phải** Đạt theo checklist vì tiêu chí 4 chưa kiểm.
- Mã lỗi trỏ sang mục 2.

| Skill | Kích hoạt | Format | Nội dung | Ổn định (chưa kiểm; rủi ro) | Dữ liệu | Kết luận | Lỗi | Đề xuất sửa |
|---|---|---|---|---|---|---|---|---|
| analyze-source-documents | Theo chữ 6/6; rủi ro C1, C3 | OK (82 dòng, 8 mục) | Chạy tay khớp mẫu mục 4 (5 câu tóm tắt, 9 RT, 8 G, 7 câu hỏi). §6, §7 của input là chi tiết tự thêm, chưa gắn nhãn | Vừa: số RT phụ thuộc cách tách câu; ranh giới "≈" và "≠" mơ hồ | Sạch | Chưa đạt | A-01 | Xem mục 7 (quyết định giữ): input.md dòng 6 thêm nhãn "tài liệu giả lập, có chủ ý lệch case `[GIẢ ĐỊNH]`". description thêm trỏ research-benchmark (C3). |
| build-glossary | Theo chữ 6/6; rủi ro cao C1 | OK (80 dòng) | 15 thuật ngữ + 4 chưa đủ nguồn khớp tiêu đề. ERP "Có nguồn rõ" nhưng input chỉ nói giá niêm yết | Cao: không có tiêu chí cứng cho "từ thông dụng bỏ qua" và cho "Có nguồn rõ / Cần xác nhận" | Sạch | Chưa đạt | A-02, A-09 | output.md dòng 19 (ERP) đổi sang "Cần xác nhận" hoặc bỏ "tồn kho, đơn hàng, công nợ" khỏi định nghĩa; dòng 20 (Công nợ quá hạn) bỏ "dữ liệu lấy từ ERP" hoặc dẫn "Bối cảnh case". SKILL.md bước 6 thêm bảng ánh xạ Loại (Fact/Rule/Nhu cầu/Ý kiến) sang trạng thái. |
| build-mind-map | Theo chữ 6/6; description trỏ chung chung | OK; Mermaid parse OK (SKILL + output); 8 nhánh, sâu 3 cấp | Khớp luật (≤8 nhánh, ≤4 cấp, bảng 8 nhánh = 8 nhánh sơ đồ). Output thêm F6, F7 mà input không có | Vừa | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | A-05 | SKILL.md dòng 3 đổi "skill vẽ flow" thành `model-business-process`. output.md dòng 46–47: ghi "F6/F7 theo case" hoặc bỏ mã. |
| design-survey-and-analyze | Theo chữ 6/6 | OK (82 dòng) | Số liệu khớp: 11 lượt chủ đề + 1 chưa xếp = 12; nhóm lớn 5 câu đúng; 12/200 = 6%. Chủ đề C2 map sang R7 chưa hợp | Vừa-cao: đặt tên chủ đề và ranh giới gán là tự do | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | A-08 | output.md dòng 35: đổi liên hệ C2 từ R7 sang R3/F5. |
| facilitate-brainstorming | Theo chữ 6/6; rủi ro C5 | OK (84 dòng) | Điểm Tác động × Khả thi tính lại đúng 14/14; 14 ý nằm đúng 1 nhóm. "Đề xuất ưu tiên" liệt kê 6 ý (B3, B1, B11, B2, B13, B5), vượt "3–5" | Cao: số ý AI thêm, điểm, cờ phạm vi đều chủ quan; chỉ có ràng buộc "AI ≤ ý của team" | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | A-06 | SKILL.md bước 7 nói rõ "tối đa 5, ý giữ mốc riêng đếm vào 5" hoặc output.md bỏ dòng 5 sang bảng riêng. |
| plan-requirements-workshop | Theo chữ 6/6 | OK (91 dòng) | Agenda cộng đúng 120 phút, đệm 18 phút = 15%. Cột "Lưu ý" và mục "Rủi ro workshop" nêu tính cách người dự trong bản chia sẻ, trái SKILL.md mục 7 | Vừa | Có nhận xét tính cách người thật trong tài liệu chia sẻ | Chưa đạt | A-07 | output.md dòng 9–12 và 56–58: tách thành mục "Ghi chú riêng cho BA (không gửi chung)" hoặc sửa SKILL.md mục 7 cho khớp. |
| prepare-stakeholder-interview | Theo chữ 6/6; rủi ro C1 | OK (82 dòng) | Câu chính Q1, Q3, Q7, Q8, Q9 là câu kép, trái bước 4 và mục 5 của chính skill. Cột "Nhóm (phút)" lặp phút theo dòng (B (15) ×3) gây khó cộng | Vừa: số câu Q không cố định (13) | Sạch | Chưa đạt | A-03, A-04 | output.md dòng 17, 19, 23, 24, 25: tách mỗi câu chính thành 1 ý, đẩy ý thứ hai xuống cột "Câu đào sâu". SKILL.md mục 4 thêm "ghi phút ở dòng đầu của nhóm". |
| model-business-process | Theo chữ 6/6; rủi ro ngoài repo (ba-flow-diagram) | Mermaid parse OK. **Sơ đồ 32 nút** (ST, S1–S19, G1–G8, EN1–EN4), vượt "khoảng 20 nút" ở bước 1. Bảng bước thiếu 5 mã (ST, EN1–EN4), trái mục 5 "mã khớp từng dòng" | Quyết định/nhánh khớp case; nhánh [GIẢ ĐỊNH] có nhãn. Stale: nói UC-01 chưa có exception ERP, trong khi write-use-case-spec đã có E3, E4 | Cao: số nút, nhánh [GIẢ ĐỊNH] của lane Kế toán, cách chia sub-process không có luật cứng | Sạch | Chưa đạt | B-02, B-04 | output.md: thêm 5 dòng bảng bước (ST, EN1–EN4) hoặc đổi quy ước; tách sơ đồ thành 2 (nhánh duyệt chiết khấu; nhánh công nợ) hoặc nâng giới hạn ở SKILL.md bước 1 lên 35. Dòng 108/121: ghi "UC-01 theo case (E1, E2); E3, E4 thêm ở write-use-case-spec". |
| write-use-case-spec | Theo chữ 6/6; rủi ro C6 | OK (92 dòng) | Đủ 8 phần, 2 A + 4 E. E3 đặt "tại bước 2 hoặc 7" (2 điểm, trái bước 6 "tại bước n"), Postcondition gộp "E3, E4 → Nháp" nhưng E3 ở bước 2 là dừng. Bước 7 ghi "một giao dịch" nhưng sequence tách hai lời gọi | Vừa: ngoài 2 A + 3 E bắt buộc, số exception "đề xuất thêm" không bị chặn trên (có thể 3–6) | Sạch | Chưa đạt | B-01, B-03, B-06 | output.md dòng 56–59, 19: tách E3 thành E3 (chỉ bước 7, khớp write-user-story-and-ac/input.md dòng 18) và E5 "ERP không phản hồi khi tải danh mục (bước 2)"; sửa Postcondition. Dòng 30: bỏ "(một giao dịch)" hoặc nêu rõ thành hai lời gọi. |
| write-user-story-and-ac | Theo chữ 6/6; rủi ro ngoài repo | OK (84 dòng) | Số học AC đúng (475.500; 475.000; 450.000; 449.500). Nhưng AC-01, AC-07, AC-08, AC-09 có nhiều hơn một When; AC chứa số hiệu năng (≤5 giây, ≤5 phút, ≤15 phút, 30 giây, ≤3 giây) trái mục 6 "hiệu năng thuộc write-nfr" | Cao: cách cắt story và số AC không có luật cứng | Sạch | Chưa đạt | C-01, C-02, C-03 | output.md dòng 12, 26–28: tách When ("rồi gửi đơn") thành Given hoặc AC riêng. Dòng 12, 16, 49, 50, 52: dẫn "theo NFR-xx" hoặc để số vào Câu hỏi mở. |
| draw-sequence-diagram | Theo chữ 6/6; rủi ro C8 | Mermaid parse OK | Mã [b1]–[b8] đủ; tên alt E1/E2/E3 trùng mã spec. Ghi "E3 tại bước 2 cùng cách xử lý" sai so với spec output (bước 2 là dừng). Tách kiểm tra công nợ / ghi đơn thành hai [b7], khác spec ("một giao dịch") | Vừa-thấp | Sạch | Chưa đạt | B-01, B-03 | output.md dòng 2 sửa lý do không vẽ E3 bước 2; dòng 36, 48 đổi nhãn thứ hai thành [b7'] hoặc sửa spec bước 7. |
| draw-state-diagram | Theo chữ 6/6 | Mermaid parse OK; T1–T13 khớp bảng 1–1 | Guard loại trừ nhau hoặc có ưu tiên rõ. Ví dụ là Yêu cầu bảo hành, không phải vòng đời đơn của UC-01 nên chuỗi UC → State chưa được thử | Vừa-cao: gộp/tách "Đang xử lý" là quyết định chủ quan (đã hỏi ở Câu hỏi mở 6) | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | B-05 | Thêm ví dụ thứ hai hoặc ghi chú: vòng đời "Đơn hàng" trích từ UC-01 để kiểm chuỗi. |
| generate-prototype-screens | Theo chữ 6/6; rủi ro ngoài repo | OK (97 dòng); Mermaid parse OK | Ma trận AC → màn hình phủ AC-01..10, 14..19, ghi rõ AC-11..13 để sau. Trạng thái đủ hoặc "không áp dụng" kèm lý do. Mã đơn "DH-0001" khác định dạng của data dictionary | Vừa-cao: số màn hình, gộp bước | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | C-04 | Thống nhất ví dụ mã (xem mục 3.4). |
| draft-data-model | Theo chữ 6/6 | Mermaid parse OK (SKILL + output) | 7 thực thể, 8 khóa ngoại, 8 quan hệ khớp ERD. Input ghi danh từ "trích glossary" nhưng 4/6 danh từ không có trong build-glossary/output.md. Checklist Q5 trả lời "Một phần", ngoài tập Có/Không/Cần hỏi | Vừa: thêm NHAN_VIEN ngoài danh sách là quyết định chủ quan (đã nêu) | Sạch (chỉ tên trường, không giá trị thật) | Chưa đạt | D-01, D-02 | input.md dòng 6: bỏ "(trích glossary)" hoặc đổi danh từ cho khớp glossary ("Dự án" thay "Dự án đã báo"; thêm "Dòng đơn", "Sản phẩm" vào glossary). output.md dòng 120: đổi "Một phần" thành "Cần hỏi". |
| build-data-dictionary | Theo chữ 6/6 | OK (83 dòng) | ERD input giống từng ký tự với output draft-data-model. DON_HANG 10 trường, DONG_DON 5 trường đủ, không thừa. `ma_san_pham` ghi hai nhãn nguồn, trái "đúng một nhãn" | Thấp-vừa | Sạch (dữ liệu mẫu bịa) | Đạt sơ bộ (kèm lỗi Thấp) | D-04 | output.md dòng 29: chọn một nhãn (`Cổng-nhập`) và đưa phần "mã dùng chung ERP" sang Giá trị hợp lệ. |
| write-nfr | Theo chữ 6/6; rủi ro C7 | OK (76 dòng) | 6 mong muốn gốc → 11 NFR, mục 1 đều có NFR ở mục 2. Input nói UC-01 chưa có exception ERP/mất mạng (cũ), trái write-use-case-spec. Số 10 giây (NFR-06) lệch AC-14 (30 giây) | Cao: ngưỡng do AI đề xuất, số NFR dao động | Sạch | Chưa đạt | D-03, C-02 | input.md dòng 16 và output.md NFR-06, Câu hỏi mở 7: cập nhật theo E3, E4. NFR-06: nêu rõ mốc "10 giây sau khi hết thời gian chờ" và dẫn AC-14. |
| analyze-business-rules | Theo chữ 6/6; rủi ro C6, C7 | OK (87 dòng) | 12 rule (5 + 7), X-01..04, G-01..05 khớp bảng. Bảng T1–T5: kết quả mức B cho T2 ("GĐ 2" so "GĐ2") không suy ra được từ định nghĩa "khoảng trắng thừa" trong rule-patterns.md | Vừa-cao | Sạch | Chưa đạt | E-03, E-05 | references/rule-patterns.md mức B: ghi "bỏ mọi khoảng trắng"; hoặc output.md dòng 53 đổi T2 thành "phụ thuộc cách chuẩn hóa". |
| pre-review-requirements | Theo chữ 6/6; rủi ro C7 | OK (80 dòng) | Bảng tóm tắt khớp 13 lỗi (đếm lại: Cao 3, TB 9, Thấp 1; theo tiêu chí 2/3/4/3/1). Mọi R1–R12 có mặt. Gợi ý trỏ đúng slug | Cao: không có luật gộp lỗi cùng gốc, nên số dòng lỗi (13) dao động | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | E-04 | input.md dòng 12: bỏ "(hồ sơ công ty)" hoặc ghi `[GIẢ ĐỊNH]`. |
| draft-swot | Theo chữ 6/6 | OK (86 dòng) | Mọi ý có ID nguồn. Hành động A-4 ("WO") dựa trên WEA-4 + STR-5, A-6 ("WT") dựa trên WEA-7 + STR-4: không đúng ma trận TOWS | Vừa | Sạch; có nhận xét hành vi cá nhân (THR-3, WEA-7) | Chưa đạt | F-01, F-02 | output.md dòng 56, 58: đổi loại hoặc đổi cơ sở (A-4 → SO hoặc thêm OPP; A-6 → thêm THR). |
| identify-risks | Theo chữ 6/6; rủi ro C4 | OK (83 dòng) | P×I và mức đúng 9/9; tổng hợp 3/5/1/0 đúng; có ứng phó, trigger, vai. RK-02 dùng "chậm phản hồi" (mô tả tính cách) trái mục 7 | Vừa-cao: P, I do AI chấm | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | F-02 | output.md dòng 19: viết "chỉ họp 1 buổi/tuần nên câu hỏi chờ nhiều tuần", bỏ "chậm phản hồi". |
| research-benchmark | Theo chữ 6/6; rủi ro C3 | OK (85 dòng) | Mọi ô có ID nguồn, "Cần xác minh" hoặc `[GIẢ ĐỊNH]` kèm cơ sở; kết luận "Chưa đủ cơ sở". Không tìm ra lỗi nội dung. Đã kiểm: 12 ô × nhãn, nguồn S1–S4, tiêu chí khớp input | Thấp-vừa: gần như xác định vì phần lớn ô là "Cần xác minh" | Sạch | Đạt sơ bộ | Không có | description thêm chiều trỏ ngược từ analyze-source-documents (C3). |
| summarize-lessons-learned | Theo chữ 6/6; rủi ro C5 | OK (83 dòng) | Đã ẩn danh (grep 0 tên người). Đề xuất sửa S-01, S-02 trỏ đúng slug và đúng số mục 2/3/5, nhưng phần nội dung đề xuất đã có sẵn ở SKILL.md đích (xem E-01). Số lần nhắc T1/T2 lẫn ý tưởng N13 và N8 | Vừa: ngưỡng "lặp lại ≥2" cứng, nhưng cách gán skill nguồn là suy luận | Sạch | Chưa đạt | E-01, E-02 | Xem E-01. |
| analyze-root-cause | Theo chữ 6/6; rủi ro C4 | Mermaid parse OK | H1–H8 nhất quán giữa sơ đồ, bảng xương cá và bảng kiểm chứng. Mục E dòng H4 dùng "log không có dòng nhắc" làm bằng chứng, trái điều chính output nói ở mục B ("trích không có dòng chưa chứng minh sự kiện không xảy ra"). Số giờ 78.7 và 31.7 khớp mine-usage-data | Vừa-cao: số H, nhánh | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | G-02 | output.md dòng 58: cột "Bằng chứng hiện có" của H4 chỉ ghi "UC-01 E2 không nêu thời hạn"; chuyển "log không có dòng nhắc" sang "Chưa có". |
| mine-usage-data | Theo chữ 6/6; rủi ro C4 | OK (79 dòng) | **Tính lại bằng Python toàn bộ số: khớp 100%** (xem 1.3). Q0 coi bản nháp (1 dòng) là "dòng lỗi", trong khi Nháp là trạng thái hợp lệ | Thấp-vừa: số do SQL quyết định; chỉ phần nhận định dao động | Sạch | Đạt sơ bộ (kèm lỗi Thấp) | G-01, G-03 | output.md dòng 12: tách "bản nháp" khỏi "dòng lỗi". Chưa chạy SQL trên PostgreSQL thật. |

### 1.3 Kết quả tính lại mine-usage-data (Python, input 17 dòng)

| Chỉ số | Output nêu | Tính lại | Khớp |
|---|---|---|---|
| Đơn đã gửi / qua cổng / tỷ lệ | 16 / 9 / 56.3 | 16 / 9 / 56.25 (PostgreSQL `ROUND` numeric làm tròn 56.3) | Có |
| Đơn Đã xác nhận / hợp lệ | 13 / 12 | 13 / 12 (loại DH-0017 vì xác nhận trước khi tạo) | Có |
| Q2 EMAIL_ZALO | 5 đơn, TB 18.80, trung vị 20.0, 0 đơn ≤4h | 5, 18.80, 20.0, 0 (giá trị: 6, 18, 20, 24, 26) | Có |
| Q2 PORTAL | 7 đơn, TB 3.43, trung vị 2.5, 5 đơn ≤4h, 71.4% | 7, 3.43, 2.5, 5, 71.4 (1.5, 1.5, 2.5, 2.5, 4, 6, 6) | Có |
| Q2 tổng | 12 đơn, 118 giờ, TB 9.83, trung vị 6.0, 5 (41.7%) | 12, 118, 9.83, 6.0, 5, 41.7 | Có |
| Q3 giờ giữ đến 18/12 17:00 | DH-0005 78.7; DH-0009 56.0; DH-0013 31.7 | 78.7; 56.0; 31.7 | Có |
| Q4 | 8 đại lý, mỗi nhóm 2 đơn (D-91bc 1+1) | Khớp | Có |
| "6/7 đơn email/Zalo thuộc 3 đại lý" | D-2e5d, D-a07f, D-e612 | 2+2+2 = 6 trên 7 | Có |
| "Đơn qua cổng 1.5 đến 6 giờ" (Câu hỏi mở 3) | 1.5–6 | min 1.5, max 6 | Có |
| Ngày | Go-live thứ Hai 07/12/2026; 14/12 thứ Hai; 18/12 thứ Sáu | Đúng | Có |

Chéo skill: root-cause (DH-0005 giữ 78.7 giờ, DH-0013 giữ 31.7 giờ, kênh PORTAL / EMAIL_ZALO, đại lý D-c40e / D-a07f) khớp mine-usage-data.

---

## 2. Danh sách lỗi theo mức độ, gom theo subagent gốc

Tóm tắt: 1 lỗi Cao, 13 Vừa, 21 Thấp (+ lỗi chéo X-xx ở mục 3 và 4). Không tìm thấy dữ liệu thật, không có Mermaid sai cú pháp, không có skill thiếu mục hoặc sai tên mục. Hầu hết lỗi nằm ở **ví dụ** (output.md/input.md) lệch SKILL.md hoặc lệch skill khác, ít lỗi ở SKILL.md.

### Cao

| ID | Subagent | Lỗi | Bằng chứng | Sửa |
|---|---|---|---|---|
| B-01 | B (và C, D nhận hệ quả) | Mã luồng **E3** không nhất quán giữa spec và các tài liệu trích dẫn. Spec đặt E3 "tại bước 2 hoặc 7" và Postcondition gộp "E3, E4 → Nháp", nhưng ở bước 2 chưa có đơn nên không thể "về Nháp". write-user-story-and-ac coi E3 chỉ ở bước 7; sequence output nói E3 tại bước 2 "cùng cách xử lý". | write-use-case-spec/examples/output.md dòng 19 và 56–59; write-user-story-and-ac/examples/input.md dòng 18 ("ERP không phản hồi khi ghi đơn (bước 7)"); draw-sequence-diagram/examples/input.md dòng 27 và output.md dòng 2. Vi phạm bước 6 "tại bước n" của write-use-case-spec/SKILL.md. | Tách: E3 chỉ ở bước 7 (đơn → Nháp); thêm E5 "ERP không phản hồi khi tải danh mục (bước 2)" (use case dừng). Cập nhật Postcondition, sequence "Không vẽ" (nêu E5 thay vì "cùng cách xử lý"), và Câu hỏi mở 5 của spec. |

### Vừa

| ID | Subagent | Lỗi | Bằng chứng | Sửa |
|---|---|---|---|---|
| A-01 | A | Chi tiết tự thêm trong input analyze-source-documents ("ngưỡng 8%", ưu tiên theo "Ngày nhận") chưa gắn nhãn là giả lập, tạo 4 phát hiện (RT-06, RT-07, RT-09, G1, G3). Xem mục 7. | input.md dòng 18 (§6) và 20 (§7); output.md dòng 15, 16, 18, 29, 35, 37, 45, 47 | Giữ nhưng gắn nhãn (mục 7). |
| A-02 | A | build-glossary gán "Có nguồn rõ" cho ERP và nói công nợ lấy từ ERP, nhưng input (Q11) chỉ nói giá niêm yết lấy từ ERP; tồn kho, đơn hàng, công nợ chỉ có trong case. | output.md dòng 19 (ERP: Q11, Q12) và 20 (Công nợ quá hạn: Q11); input.md Q11 | Đổi trạng thái thành "Cần xác nhận" hoặc ghi nguồn "Bối cảnh case". Vi phạm mục 5 của chính skill ("Có nguồn rõ chỉ khi nguồn nói trực tiếp"). |
| A-03 | A | Câu chính của interview là câu kép (Q1, Q3, Q7, Q8, Q9), trái bước 4 ("tránh câu kép") và mục 5. | prepare-stakeholder-interview/examples/output.md dòng 17, 19, 23, 24, 25 | Mỗi câu chính một ý; ý sau chuyển sang "Câu đào sâu". |
| B-02 | B | model-business-process: sơ đồ 32 nút (ST + S1–S19 + G1–G8 + EN1–EN4), vượt "khoảng 20 nút" (bước 1); bảng bước thiếu ST và EN1–EN4 (mục 5: "mã S, G, EN khớp từng dòng của bảng bước"). Đã đếm bằng script. | model-business-process/SKILL.md dòng 20 và 71; output.md dòng 77–104 | Thêm 5 dòng bảng; tách sơ đồ thành quy trình chính + 2 quy trình con. |
| B-03 | B | Spec bước 7 là "một giao dịch" (kiểm tra công nợ và ghi đơn), nhưng sequence tách hai lời gọi và đánh cả hai là `[b7]`, nêu là `[GIẢ ĐỊNH]` trong khi spec là nguồn. | write-use-case-spec/examples/output.md dòng 30; draw-sequence-diagram/examples/output.md dòng 36, 48, 67, 72 | Chọn một: spec bước 7 viết thành 7a/7b, hoặc sequence gộp một lời gọi. |
| C-01 | C | AC có nhiều hơn một When: AC-01 (thêm 5 cuộn, chọn địa chỉ, rồi gửi), AC-07, AC-08, AC-09 ("xin chiết khấu ..., rồi gửi đơn"). | write-user-story-and-ac/SKILL.md dòng 25 và mục 5; output.md dòng 12, 26, 27, 28 | Đưa hành động đầu vào Given; mỗi AC một When. |
| C-02 | C, D | AC chứa chỉ số hiệu năng và thời gian (≤5 giây, ≤5 phút, ≤15 phút, 30 giây, ≤3 giây) trong khi mục 6 nói hiệu năng thuộc write-nfr. Số lệch NFR: AC-14 (ERP chờ 30 giây) so với NFR-06 ("thông báo trong ≤10 giây" từ lúc ERP quá hạn); AC-17 (≤3 giây) trùng ý NFR-01 (LCP ≤3,0 giây) nhưng chỉ số khác (khung màn hình vs LCP). | AC-01, 05, 14, 15, 17 (output.md dòng 12, 16, 49, 50, 52); write-nfr/examples/output.md NFR-01, NFR-06 | AC dẫn "theo NFR-xx" thay vì tự đặt số, hoặc ghi rõ AC-17 là phần chức năng (chỉ báo đang tải) còn con số do NFR-01 quy định. |
| D-01 | D | draft-data-model input ghi danh từ "trích glossary" nhưng glossary của skill A không có "Dự án đã báo", "Dòng đơn", "Sản phẩm", "Phê duyệt chiết khấu" (có "Dự án", "Báo dự án", "Duyệt chiết khấu"). Chuỗi Glossary → Data model dùng tên khác nhau. | draft-data-model/examples/input.md dòng 6–7; build-glossary/examples/output.md dòng 7–21 | Đổi nhãn "(trích glossary)" thành "(rút từ spec)", hoặc đồng bộ tên. |
| D-03 | D (và B) | write-nfr và model-business-process còn viết "UC-01 chưa có exception ERP không phản hồi/mất mạng", trong khi write-use-case-spec đã có E3, E4. NFR-06, NFR-07 và Câu hỏi mở 7 đề nghị "bổ sung" thứ đã có. | write-nfr/examples/input.md dòng 16, output.md NFR-06 và Câu hỏi mở 7; model-business-process/examples/output.md dòng 108, 121 | Nêu rõ "UC-01 theo case (E1, E2)" hoặc trỏ E3, E4 của write-use-case-spec. |
| E-01 | E | summarize-lessons-learned đề xuất "thêm" vào SKILL.md đích những điều đã có: write-use-case-spec bước 5 đã yêu cầu tìm exception "hệ thống ngoài lỗi, mất mạng" và bước 7 đề xuất thêm; write-user-story-and-ac bước 5 đã yêu cầu AC lỗi cho mỗi exception, mục 5 đã yêu cầu `[GIẢ ĐỊNH]` cho số; generate-prototype-screens bước 6 đã nêu dữ liệu minh họa gắn `[GIẢ ĐỊNH]`. Số mục (2, 3, 5) đúng, nhưng nội dung đề xuất trùng. | summarize-lessons-learned/examples/output.md dòng 28–29; write-use-case-spec/SKILL.md dòng 24, 26; write-user-story-and-ac/SKILL.md dòng 24, 62; generate-prototype-screens/SKILL.md dòng 26 | SKILL.md của summarize-lessons-learned bước 7 thêm "đọc lại mục đích trong SKILL.md đích; nếu quy tắc đã có thì đề xuất làm cứng hơn (ví dụ quy tắc đếm, ví dụ sai), không đề xuất lặp". |
| E-03 | E | Bảng thử BR-D1: kết quả T2 mức B ("GĐ 2" so "GĐ2") là "Trùng" nhưng định nghĩa mức B chỉ bỏ "khoảng trắng thừa", trong khi "GĐ 2" có đúng một khoảng trắng (thừa so với "GĐ2" chứ không phải khoảng trắng đôi). Kết quả phụ thuộc cách cài chuẩn hóa, nên không tái lập được. | analyze-business-rules/references/rule-patterns.md mục "So khớp dữ liệu" dòng mức B; examples/output.md dòng 53 | Mức B: "bỏ mọi khoảng trắng, hoa/thường và dấu". |
| F-01 | F | draft-swot gán loại TOWS sai: A-4 "WO" dựa trên WEA-4 và STR-5 (không có Opportunity); A-6 "WT" dựa trên WEA-7 và STR-4 (không có Threat). | draft-swot/examples/output.md dòng 56, 58; SKILL.md bước 7 | A-4 → "SO" hoặc thêm OPP; A-6 → thêm THR hoặc đổi loại. |
| X-01 | A–G | Rule đặt hàng và chiết khấu chưa có mã BR; ba skill dùng ba cách: "chưa có mã" (write-use-case-spec), BR-C1…C7 (analyze-business-rules), "business rule chiết khấu" không mã (write-user-story-and-ac, draft-data-model). Hệ quả: truy vết AC → rule và UC → rule không thể máy hóa. | Xem mục 3.3 | Dùng bảng mã BR-O…, BR-F… ở mục 3.3 và đưa vào `_shared`. |

### Thấp

| ID | Subagent | Lỗi | Bằng chứng | Sửa |
|---|---|---|---|---|
| A-04 | A | Cột "Nhóm (phút)" lặp phút theo dòng (B (15) × 3) nên cộng thô ra 195 chứ không phải 60. | prepare-stakeholder-interview/output.md dòng 17–29 | Ghi phút ở dòng đầu của nhóm. |
| A-05 | A | build-mind-map: description trỏ "skill vẽ flow"; output dùng mã F6, F7 không có trong input. | SKILL.md dòng 3; output.md dòng 46–47; input.md dòng 4 | Trỏ `model-business-process`; ghi "F6, F7 theo case". |
| A-06 | A | facilitate-brainstorming: "Đề xuất ưu tiên" liệt kê 6 ý, SKILL bước 7 nói 3–5. | output.md dòng 49–53 | Đưa B5 sang dòng "mốc riêng" ngoài danh sách ưu tiên. |
| A-07 | A | plan-requirements-workshop đưa nhận xét tính cách (hay thêm yêu cầu, thiên về đại lý lớn) vào bản chia sẻ, trái SKILL mục 7. | output.md dòng 9–12 và 56–58; SKILL.md dòng 82 | Tách phụ lục "chỉ BA". |
| A-08 | A | design-survey: chủ đề C2 (chờ duyệt chiết khấu) liên hệ R7 (mật khẩu, lưu vết) chưa hợp. | output.md dòng 35 | Liên hệ R3 hoặc F5. |
| A-09 | A | build-glossary input không đồng bộ với khung biên bản (tên chủ đề Q2–Q4 "Báo dự án hiện tại" thành "Báo dự án"; Q10 "Duyệt chiết khấu" thành "Chiết khấu"); SKILL nói dùng được cột "Loại" nhưng không có quy tắc đổi Loại sang Trạng thái; input ghi ~200 và ~300 đại lý không đối chiếu. | build-glossary/examples/input.md dòng 3, 10–15; prepare-stakeholder-interview/examples/output.md dòng 47–53 | Thêm bảng ánh xạ (mục 3.2). |
| B-04 | B | Xem D-03 (phần model-business-process). | | |
| B-05 | B | draw-state-diagram: ví dụ chỉ là Yêu cầu bảo hành; không có ví dụ nào cho vòng đời Đơn hàng (Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận), nên chuỗi UC-01 → State chưa được thử; output không trích mã UC. | draw-state-diagram/examples/output.md | Thêm ví dụ hoặc cột "Luồng UC" trong bảng chuyển. |
| B-06 | B | write-use-case-spec: A1 có hai điểm kết thúc (dưới 5% quay lại bước 5; từ 5% sang "Chờ duyệt chiết khấu"), tiêu đề chỉ nêu một; mô tả việc duyệt của F5 xen vào A1. | output.md dòng 34–38 | Tách A1 (xin chiết khấu) và A3 (đại lý tự áp dưới ngưỡng), hoặc ghi hai điểm kết thúc. |
| C-03 | C | US-03 (duyệt chiết khấu, F5) nằm trong tài liệu UC-01 và truy vết "A1", trong khi spec nói việc duyệt là use case riêng chưa có mã. | write-user-story-and-ac/examples/output.md dòng 31–40; write-use-case-spec output.md dòng 38 | Ghi "UC-02 (F5, chưa viết) / A1 bước 3". |
| C-04 | C, D, G | Ví dụ mã không thống nhất: mã đơn DH-0001 (C, G) so với DH-2026-000101 (D); sản phẩm CAP-0001 (C) so với SP-0001 (D); mã dòng DD-…. | generate-prototype-screens/examples/output.md dòng 139; build-data-dictionary/examples/output.md | Chọn một dạng (mục 3.4). |
| D-02 | D | draft-data-model checklist Q5 trả lời "Một phần", ngoài tập Có/Không/Cần hỏi. | output.md dòng 120 | "Cần hỏi". |
| D-04 | D | build-data-dictionary: `ma_san_pham` ghi hai nhãn nguồn, trái "đúng một nhãn". | output.md dòng 29; SKILL.md mục 5 | Một nhãn. |
| E-02 | E | summarize-lessons-learned: T1 đếm N13 (ý tưởng) là lần nhắc; T2 đếm N8 dù O-01 coi N8 là "mới thấy một lần". | output.md dòng 7–8, 34 | Đếm theo nhãn Chưa tốt. |
| E-04 | E | pre-review input tự đặt nguồn "hồ sơ công ty" cho ~200 đại lý; case không nêu nguồn. | pre-review-requirements/examples/input.md dòng 12 | Bỏ "(hồ sơ công ty)". |
| E-05 | E | analyze-business-rules: BR-C1 gộp 3 mức nên không "nguyên tử" (bù bằng bảng quyết định). | output.md dòng 14; SKILL.md bước 2 | Ghi chú "rule bảng quyết định". |
| F-02 | F | Mô tả tính cách trong tài liệu chia sẻ: RK-02 "chậm phản hồi"; THR-3 "được TP Quản lý kênh bảo vệ"; WEA-7 "ngại ảnh hưởng ERP". Trái mục 7 của identify-risks và draft-swot. | identify-risks/examples/output.md dòng 19; draft-swot/examples/output.md dòng 47, 34 | Nêu ràng buộc quy trình thay cho tính cách. |
| G-01 | G | mine-usage-data Q0 đặt "mong đợi 0 dòng lỗi" nhưng đếm cả bản nháp (hợp lệ). | output.md dòng 12, 80 | Tách "bản nháp". |
| G-02 | G | analyze-root-cause dùng "log không có dòng nhắc" làm bằng chứng cho H4, mâu thuẫn mục B. | output.md dòng 15 và 58 | Chuyển sang "Chưa có". |
| G-03 | G | SQL của mine-usage-data chưa chạy trên PostgreSQL thật (chỉ tính lại bằng Python). | | BA chạy theo mục 6 của skill. |
| X-02 | Tất cả | Mức độ dùng ba thang chữ khác nhau: Cao/Trung bình/Thấp (pre-review, analyze-business-rules), Rất cao/Cao/Trung bình/Thấp (identify-risks), Cao/Vừa/Thấp (báo cáo này). | | Thống nhất Cao / Trung bình / Thấp; "Rất cao" chỉ riêng thang 5×5. |

### Gom theo subagent gốc (để giao sửa 1 vòng)

| Subagent | Skill | Lỗi cần sửa (ưu tiên từ trên xuống) |
|---|---|---|
| A (01-elicitation) | 7 skill | A-01, A-02, A-03 (Vừa); A-04, A-05, A-06, A-07, A-08, A-09 (Thấp). Chỉ sửa ở output.md/input.md và 1 dòng description của build-mind-map, trừ đề xuất description ở mục 1B (C1, C3, C5). |
| B (model-business-process, write-use-case-spec, draw-sequence-diagram, draw-state-diagram) | 4 skill | B-01 (Cao); B-02, B-03 (Vừa); B-05, B-06, B-04 (Thấp). B-01 và B-03 phải sửa đồng bộ cả spec lẫn sequence. |
| C (write-user-story-and-ac, generate-prototype-screens) | 2 skill | C-01, C-02 (Vừa); C-03, C-04 (Thấp). Sau khi B sửa E3/E5, C cập nhật input và ma trận phủ. |
| D (draft-data-model, build-data-dictionary, write-nfr) | 3 skill | D-01, D-03 (Vừa); D-02, D-04 (Thấp). Phối hợp C về NFR-06 ↔ AC-14 (C-02). |
| E (pre-review-requirements, analyze-business-rules, summarize-lessons-learned) | 3 skill | E-01, E-03 (Vừa); E-02, E-04, E-05 (Thấp). X-01: E đề xuất mã BR chính thức (mục 3.3). |
| F (04-strategy) | 3 skill | F-01 (Vừa); F-02 (Thấp). research-benchmark không có lỗi tìm được. |
| G (06-solution-evaluation) | 2 skill | G-01, G-02, G-03 (Thấp). Số liệu mine-usage-data và liên kết với analyze-root-cause đã khớp. |

---

## 3. Tính nhất quán giữa các skill

### 3.1 Giọng văn, tên 8 mục, nhãn

| Hạng mục | Kết quả đo | Mức |
|---|---|---|
| Tên và thứ tự 8 mục SKILL.md | 24/24 giống template (script) | Nhất quán |
| Mục 7 có "ẩn danh" và `[GIẢ ĐỊNH]` | 24/24 (script) | Nhất quán |
| Mục 1 (Mục đích) diễn đạt lại, không chép sách | Đọc cả 24: văn tự viết, có nêu BABOK; không thấy chép nguyên văn | Nhất quán |
| Cách viết người trả lời ở "Câu hỏi mở" | Đếm trên 24 output.md: `(cần: X)` ở 7 skill 01-elicitation; `(Tên)` cuối câu ở draft-data-model, build-data-dictionary, write-use-case-spec, draw-sequence-diagram, draw-state-diagram, model-business-process, write-nfr, draft-swot, identify-risks, research-benchmark; `— cần X` ở write-user-story-and-ac, generate-prototype-screens; `Tên: câu hỏi` ở analyze-business-rules, pre-review-requirements, summarize-lessons-learned; `Cần X` ở analyze-root-cause, mine-usage-data | **Lệch: 5 kiểu.** Đề xuất một kiểu: `(cần: <vai hoặc tên>)` cuối câu, đúng như mẫu `_template` mục 8 ("ghi rõ cần ai trả lời"). |
| Cách gọi nhân vật | 01-elicitation viết thường "anh Quang / chị Hạnh" (lowercase 14 lần ở analyze-source-documents); 02-radd, 03-rlcm viết hoa "Anh Quang / Chị Hạnh"; 04-strategy, 05, 06 chủ yếu dùng vai ("Giám đốc Kinh doanh", "Kế toán trưởng"). | Lệch. Đề xuất: lần đầu "Anh Quang (Giám đốc Kinh doanh)", sau đó chữ hoa "Anh Quang". Skill chia sẻ rộng (risk register, retro) dùng vai. |
| Mức độ | Cao / Trung bình / Thấp (pre-review, analyze-business-rules); thêm "Rất cao" (identify-risks); "Cao/Vừa/Thấp" chỉ ở báo cáo này | Đề xuất: Cao / Trung bình / Thấp; "Rất cao" chỉ dùng cho thang 5×5. |
| Dấu "kết thúc đầu ra bằng Câu hỏi mở" | 24/24, mẫu mục 4 cũng kết thúc bằng mục đó | Nhất quán |

### 3.2 Nhãn trạng thái nguồn: hai hệ đang chạy song song

| Hệ | Nơi dùng | Giá trị |
|---|---|---|
| "Độ chắc của nguồn" | build-glossary: `Có nguồn rõ · Cần xác nhận · [GIẢ ĐỊNH]`; draft-swot: `Có nguồn · [GIẢ ĐỊNH] · Cần xác minh`; research-benchmark: ID nguồn · `Cần xác minh` · `[GIẢ ĐỊNH]` | 3 giá trị, nhưng tên khác nhau: "Cần xác nhận" so với "Cần xác minh"; "Có nguồn rõ" so với "Có nguồn" |
| "Loại phát ngôn" | prepare-stakeholder-interview: `Fact · Rule · Nhu cầu · Ý kiến`; analyze-source-documents: `Rõ / Mơ hồ` và `= ≈ ≠ Mới` | khác nhau về bản chất (loại thông tin, không phải độ chắc) |
| "Độ xác lập giả thuyết" | analyze-root-cause: `Chưa kiểm chứng`; mine-usage-data: `Chưa đối chiếu / Lệch chưa giải thích` | trạng thái việc cần làm |

**Đề xuất tối thiểu (thêm vào `_shared`):**
1. Một trục "Độ chắc nguồn" dùng đúng ba giá trị `Có nguồn` · `Cần xác minh` · `[GIẢ ĐỊNH]`. Đổi build-glossary "Có nguồn rõ" thành "Có nguồn", "Cần xác nhận" thành "Cần xác minh" (3 chỗ: SKILL.md dòng 24, 33, 59; references/glossary-conventions.md bảng Trạng thái).
2. Trục "Loại phát ngôn" (Fact/Rule/Nhu cầu/Ý kiến) chỉ dùng trong biên bản phỏng vấn. Khi chuyển sang glossary: Fact hoặc Rule do người có thẩm quyền nói → `Có nguồn`; Ý kiến hoặc một người nói → `Cần xác minh`; Nhu cầu → không dùng làm định nghĩa. Ghi quy tắc này ở build-glossary bước 6.
3. Trạng thái việc cần làm (`Chưa kiểm chứng`, `Chưa đối chiếu`, `Chưa phủ`, `Chưa họp`) giữ riêng, không trộn với trục 1.

### 3.3 Mã BR cho rule đặt hàng và chiết khấu

Hiện có: BR-D1…D5 (báo dự án, trong case). Rule đặt hàng và chiết khấu trong case chưa có mã: write-use-case-spec ghi "chưa có mã" (6 dòng, output.md dòng 68–73); analyze-business-rules tự gán BR-C1…C7 ở dạng mã tạm; write-user-story-and-ac, draft-data-model, generate-prototype-screens trích "business rule chiết khấu" không mã. Đề xuất chính thức hóa mã của analyze-business-rules (ít sửa nhất) và thêm một mã cho phân quyền:

| Mã đề xuất | Nội dung (case) | Loại | Tương ứng hiện tại |
|---|---|---|---|
| BR-C1 | Chiết khấu dưới 5% đại lý tự áp; 5%–10% TP Quản lý kênh duyệt; trên 10% Giám đốc Kinh doanh duyệt `[GIẢ ĐỊNH]` ngưỡng | Behaviour | BR-C1 của analyze-business-rules |
| BR-C2 | Giá niêm yết và tồn kho luôn lấy từ ERP | Behaviour | BR-C2 (cùng R6) |
| BR-C3 | Chiết khấu tính trên giá niêm yết, áp cả đơn | Definition | BR-C3 |
| BR-C4 | Mỗi lần xin chiết khấu phải có lý do | Behaviour | BR-C4 |
| BR-C5 | Quyết định chiết khấu lưu kèm người duyệt và thời điểm | Behaviour | BR-C5 (cùng R7) |
| BR-C6 | Đơn chưa duyệt chiết khấu thì chưa ghi vào ERP | Behaviour | BR-C6 |
| BR-C7 | Đại lý quá hạn công nợ: đơn giữ lại, Kế toán được thông báo | Behaviour | BR-C7 (cùng R11) |
| BR-P1 | Phân quyền theo vùng (chưa có văn bản) `[GIẢ ĐỊNH]` | Behaviour | "nguyên tắc phân quyền" chưa mã trong pre-review, analyze-business-rules, draft-data-model |

Chữ C nghĩa là "Commerce": nhóm rule đặt hàng và chiết khấu. Việc cần làm: thêm vào `_shared/case-dai-viet-electric.md` mục "Business rules đặt hàng và chiết khấu"; write-use-case-spec/output.md mục 8 đổi 6 chữ "chưa có mã" thành BR-C2…C7; write-user-story-and-ac, draft-data-model, generate-prototype-screens, build-data-dictionary trích BR-Cx thay "business rule chiết khấu".

### 3.4 Bộ mã tự đặt và chỗ va chạm

Các mã sau lấy từ SKILL.md và output.md (grep các tiền tố). Cột "Va chạm" nêu cùng tiền tố khác nghĩa.

| Tiền tố hiện tại | Nghĩa hiện tại | Skill (subagent) | Va chạm |
|---|---|---|---|
| R1–R12, F1–F9, UC-01, BR-D1–D5, US-xx, AC-xx | Mã của case | toàn bộ | Không va chạm. Giữ. |
| Q1–Q13 | Câu hỏi phỏng vấn / nguồn trong biên bản | prepare-stakeholder-interview, build-glossary (A) | **Q0–Q4** là câu hỏi phân tích dữ liệu (mine-usage-data, G); **QĐ-01** là quyết định workshop (A) |
| S1, S2… | Nguồn (swot, risks, benchmark: F) | F | **S1–S19** bước quy trình (model-business-process, B); **S1–S11** câu hỏi khảo sát (design-survey, A); **S-01** lỗi AI (summarize-lessons-learned, E); `§n` đoạn tài liệu (A) |
| G1–G8 | Chỗ thiếu/mâu thuẫn (analyze-source-documents, A) | A | **G1–G8** gateway (B); **G-01…05** khoảng trống rule (analyze-business-rules, E) |
| X1–X5, X-01…04 | Xung đột cách dùng từ (glossary, A) / mâu thuẫn rule (E) | A, E | Cùng nghĩa "xung đột", khác dạng viết (X1 so với X-01) |
| T1–T13 | Chuyển trạng thái (draw-state-diagram, B) | B | **T01–T12** câu trả lời khảo sát (A); **T1–T5** cặp thử (analyze-business-rules, E); **T1–T7** chủ đề retro (E) |
| C1–C5 | Chủ đề trả lời mở (design-survey, A) | A | **C1–C6** tiêu chí (research-benchmark, F); **BR-C1…C7** (E, đề xuất giữ) |
| A1, A2 | Alternative flow (B) | B | **A-01…06** hành động retro (E); **A-1…7** hành động TOWS (F); **A, B, C** mức so khớp (E) và phương án A/B/C (workshop A) |
| B1–B14 | Ý brainstorm (A) | A | Không va chạm, trừ chữ B là tên subagent trong báo cáo này |
| N1–N4 | Nhóm ý brainstorm (A) | A | **N1–N14** ghi chú retro (E) |
| E1–E4 | Exception (B) | B | Chữ E là tên subagent trong quy ước báo cáo; không va chạm trong skill |
| EN1–EN4, ST | Điểm kết thúc / bắt đầu (B) | B | Không |
| H1–H8 | Giả thuyết nguyên nhân (G) | G | Không |
| [b1]–[b8] | Mã bước trong sequence (B) | B | Không |
| L-01… | Lỗi pre-review (E) | E | Không |
| RK-01…, STR-/WEA-/OPP-/THR-, PA-A/B | Rủi ro; ý SWOT; phương án (F) | F | Không |
| NFR-01… | NFR (D) | D | Không |
| SCR-01… | Màn hình (C) | C | Không |
| RT-01… | Rule tạm từ tài liệu (A) | A | Không |
| BR-C1…C7 | Rule đặt hàng và chiết khấu (E, tạm) | E | Xem 3.3 |
| INC-014, DH-…, CAP-…, SP-…, DD-…, DL-… | Mã ví dụ (ticket, đơn, sản phẩm, dòng đơn, đại lý) | C, D, G | **DH-0001 so với DH-2026-000101**; **CAP-0001 so với SP-0001** |

**Bảng "Quy ước mã" đề xuất để thêm vào `_shared` (đổi tối thiểu):**

| Loại | Tiền tố chuẩn | Ví dụ | Đổi từ |
|---|---|---|---|
| Nhu cầu / tính năng / use case / rule | R, F, UC-, BR-D, BR-C, BR-P | R9, F5, UC-01, BR-D1, BR-C1 | Giữ |
| Story, AC, màn hình | US-, AC-, SCR- | US-03, AC-07, SCR-01 | Giữ |
| Câu hỏi phỏng vấn | Q | Q5 | Giữ |
| Câu hỏi phân tích dữ liệu | M | M0, M1 | Q0–Q4 trong mine-usage-data |
| Câu hỏi khảo sát | SQ | SQ1 | S1–S11 trong design-survey |
| Câu trả lời khảo sát | TL | TL01 | T01–T12 |
| Chủ đề (khảo sát, retro) | TM | TM1 | C1–C5 (survey), T1–T7 (retro) |
| Nguồn tài liệu | S | S1 | Giữ (swot, risks, benchmark) |
| Bước quy trình | P | P1…P19 | S1–S19 trong model-business-process |
| Gateway / điểm kết thúc / bắt đầu | GW, EN, ST | GW1, EN1 | G1–G8 (gateway) |
| Chỗ thiếu hoặc mâu thuẫn | GAP- | GAP-01 | G1–G8 (analyze-source-documents), G-01…05 (analyze-business-rules) |
| Xung đột (từ, rule) | X- | X-01 | X1–X5 (glossary) |
| Alternative / Exception | A, E | A1, E2 | Giữ |
| Mã bước trong sequence | [bN] | [b7] | Giữ |
| Chuyển trạng thái | T | T1 | Giữ (đổi T01–T12, T1–T5 của skill khác) |
| Cặp thử so khớp | TP | TP1 | T1–T5 (analyze-business-rules) |
| Ý brainstorm / nhóm ý | B / GR | B1, GR1 | N1–N4 (brainstorm nhóm) |
| Ghi chú retro / hành động / lỗi AI / lỗi theo dõi | N / ACT- / AIE- / AIW- | N4, ACT-01, AIE-01, AIW-01 | A-01 (retro), S-01, O-01 |
| Hành động TOWS | TOWS- | TOWS-1 | A-1…7 |
| Quyết định workshop | DEC- | DEC-01 | QĐ-01 |
| Giả thuyết; lỗi pre-review; rủi ro; NFR; phương án; tiêu chí | H, L-, RK-, NFR-, PA-, C | H1, L-01, RK-01, NFR-01, PA-A, C1 | Giữ |
| Ví dụ mã đơn, sản phẩm | DH-yyyy-nnnnnn, SP-nnnn | DH-2026-000101, SP-0001 | DH-0001, CAP-0001 |

Đề xuất sửa hàng loạt này nặng hơn mức "sửa tối đa 1 vòng"; nếu chỉ làm tối thiểu, ưu tiên 3 va chạm gây hiểu nhầm nhất: **G** (gateway so với gap), **S** (nguồn so với bước so với câu hỏi khảo sát), **T** (transition so với câu trả lời, cặp thử, chủ đề). Còn lại ghi chú trong `_shared` rằng mã có phạm vi theo skill.

### 3.5 Ký hiệu đánh giá

`✓ ⚠ ✗` chỉ xuất hiện ở write-user-story-and-ac (SKILL.md, output.md và references/invest-checklist.md) cho INVEST. Mọi skill khác dùng chữ (Có/Không/Cần hỏi; Đủ/Chưa đủ; Rõ/Mơ hồ; Khớp/Gần khớp/Mâu thuẫn bằng `= ≈ ≠`; Cao/Trung bình/Thấp). Không thấy chỗ nào dùng cùng ký hiệu với nghĩa khác. Đề xuất: giữ như hiện tại, ghi vào `_shared` rằng `✓ ⚠ ✗` chỉ dùng cho chấm đạt/có điều kiện/không đạt (INVEST, bảng chấm skill), các trường hợp khác dùng chữ. Phần checklist `_checklist/skill-quality.md` dùng "Đạt / Chưa đạt" bằng chữ, nhất quán với đề xuất này.

---

## 4. Kiểm chuỗi nối tiếp (mở thật hai đầu của mỗi cặp)

Chuỗi chính: Interviews → Glossary → Use Case → User Story/AC → Sequence/State. Mỗi dòng: đầu ra của skill trước, đầu vào của skill sau, kết quả.

| # | Cặp | Đã so với nhau | Kết quả | Lệch ở đâu (bằng chứng) |
|---|---|---|---|---|
| 1 | prepare-stakeholder-interview → build-glossary | Khung biên bản (`Mã Q, Chủ đề, Điều đã nghe, Loại, Rule/nhu cầu liên quan, Cần xác nhận`) với bảng biên bản trong input glossary; bảng "Thuật ngữ cần chốt" (8 từ) với bảng glossary | **Khớp một phần** | Cột khớp 6/6 và Q1–Q13 khớp. Cả 8 từ cần chốt đều có mặt trong glossary (Trùng thành "Dự án trùng", Duyệt tách thành "Duyệt dự án" và "Duyệt chiết khấu"). Lệch nhẹ: tên chủ đề đổi (Q2–Q4 "Báo dự án hiện tại" thành "Báo dự án"; Q10 "Duyệt chiết khấu" thành "Chiết khấu"; Q11 "Gõ lại đơn vào ERP" thành "Đơn hàng và ERP"). Input glossary không kèm bảng "Thuật ngữ cần chốt" nên skill chưa dùng đúng đường truyền. Cột "Loại" (Fact/Rule/Ý kiến) không được ánh xạ sang "Trạng thái" (A-09). |
| 2 | build-glossary → write-use-case-spec | "Gợi ý chuyển tiếp" với tên trạng thái, actor, luồng của UC-01 | **Khớp một phần** | Glossary dẫn đúng E2, A1 và hai trạng thái "Chờ kế toán xử lý", "Chờ duyệt chiết khấu" (khớp spec). Lệch: glossary đặt tên chuẩn "Công nợ quá hạn" còn spec/case dùng "Quá hạn công nợ"; glossary đề xuất "Sales admin → actor UC-01" nhưng spec UC-01 không có actor Sales admin; "Giữ đơn" không xuất hiện trong spec (spec dùng "đơn giữ"/"Chờ kế toán xử lý"). write-use-case-spec không đưa glossary vào đầu vào ví dụ (mục 2 chỉ ghi tùy chọn). |
| 3 | write-use-case-spec → write-user-story-and-ac | Mã luồng A1, A2, E1–E4 và bước 1–8 với cột "Luồng UC" và ma trận phủ | **Lệch nhỏ nhưng quan trọng** | A1, A2, E1, E2, E4 và Main 1–8 khớp từng mã. **E3**: spec đặt "tại bước 2 hoặc 7", US input chỉ bước 7 (B-01). Rule đặt hàng và chiết khấu: spec "chưa có mã", US trích "business rule" không mã (X-01). US-03 gắn "A1" cho việc duyệt của F5 trong khi spec nói F5 là use case riêng (C-03). Input US là "bản tóm lược" của spec chứ không phải output thật của skill B (có vẻ hai nhóm viết song song, chưa xác minh). |
| 4 | write-use-case-spec → draw-sequence-diagram | Bước 1–8 với `[b1]`–`[b8]`; tên E1–E3 với tên khối `alt`; actor | **Khớp mã, lệch nghĩa** | Mã bước và mã luồng được trích đúng. Lệch: tên E1 "Không đủ tồn kho" (spec) so với "Số lượng vượt tồn kho" (sequence); tên participant "Hệ thống" (spec) so với "Cổng đại lý"; bước 7 "một giao dịch" (spec) so với hai lời gọi (sequence, B-03); E3 bước 2 "dừng" (spec) so với "cùng cách xử lý" (sequence, B-01). |
| 5 | write-use-case-spec / write-user-story-and-ac → draw-state-diagram | Tên trạng thái đơn (Nháp, Chờ duyệt chiết khấu, Chờ kế toán xử lý, Đã xác nhận) với state diagram | **Chưa kiểm được trên ví dụ** | Ví dụ state diagram dùng Yêu cầu bảo hành (Phase 2) nên không trích mã UC hay AC nào. Không có sơ đồ trạng thái cho Đơn hàng để so với spec, US, data dictionary và prototype (B-05). Bốn trạng thái đơn xuất hiện nhất quán ở UC, US, dictionary, prototype, mine-usage-data; thiếu ở mọi nơi: trạng thái sau "Đã xác nhận" và khi chiết khấu bị từ chối. |
| 6 | write-user-story-and-ac → generate-prototype-screens | Bảng Story/AC trong input prototype với output US | **Khớp** | AC-01…AC-10 và AC-14…AC-19 đúng nội dung, đúng luồng; US-03 (AC-11–13) loại ra có ghi lý do; số học 465.000 đ cho 7% đúng. |
| 7 | glossary → draft-data-model | Danh từ "trích glossary" với bảng glossary | **Lệch** | 4/6 danh từ không có trong glossary (D-01). |
| 8 | draft-data-model → build-data-dictionary | ERD (so từng ký tự), tên thực thể và trường, số trường | **Khớp** | ERD giống hệt; DON_HANG 10 trường, DONG_DON 5 trường, đúng tên, đúng 4 giá trị trạng thái; ngưỡng đúng bậc khớp AC-07/08. Lệch nhỏ: định dạng mã đơn `DH-2026-000101` (dictionary) so với `DH-0001` (prototype, mine-usage-data); một trường ghi hai nhãn nguồn (D-04). |
| 9 | write-user-story-and-ac / write-use-case-spec → write-nfr | E3/E4, các chỉ số thời gian | **Lệch** | write-nfr nói UC-01 chưa có exception ERP/mất mạng (D-03); AC-14 (30 giây) so với NFR-06 (10 giây); AC-17 so với NFR-01 (C-02). |
| 10 | case R1–R12, BR-D1…D5 → pre-review / analyze-business-rules / identify-risks | Bảng R trong input pre-review so với case; BR-D trong 3 skill | **Khớp** | pre-review chép đúng 12 dòng R (người nêu và nội dung); analyze-business-rules và identify-risks dẫn đúng R1, R4, R5, R8, R9, R11, R12 và BR-D1…D5. Các phát hiện trùng nhau và nhất quán: L-01 ≈ X-01 (R9 so với BR-D5), L-05 ≈ X-03 (R4 so với BR-D4), L-07 ≈ G-04 (R11, quá hạn). |
| 11 | analyze-business-rules → write-use-case-spec / write-user-story-and-ac | "Rule sẵn sàng chuyển tiếp: BR-C2, BR-C3, BR-C6" | **Chưa nối được** | write-use-case-spec và write-user-story-and-ac không dùng BR-Cx (X-01). Mã BR-Cx chỉ sống trong output của analyze-business-rules. |
| 12 | summarize-lessons-learned → skill đích | Slug và số mục SKILL.md trong đề xuất sửa | **Khớp slug và số mục; trùng nội dung** | write-user-story-and-ac, generate-prototype-screens, write-use-case-spec, draw-state-diagram, build-glossary đều tồn tại; mục 2, 3, 5 tồn tại. Nhưng nội dung đề xuất đã có trong SKILL.md đích (E-01). Bảng tra trong references/ai-error-taxonomy.md có đủ 24 slug. |
| 13 | mine-usage-data ↔ analyze-root-cause | DH-0005, DH-0013, giờ giữ, kênh, mã đại lý | **Khớp** | 78.7 giờ và 31.7 giờ khớp; kênh PORTAL / EMAIL_ZALO và mã đại lý D-c40e, D-a07f khớp; R1 (4 giờ) dùng nhất quán; root-cause đề nghị lấy dữ liệu từ mine-usage-data (F), mine-usage-data đề nghị chuyển analyze-root-cause (G). |
| 14 | identify-risks → research-benchmark | RK-03 trỏ research-benchmark; ngữ cảnh nền tảng | **Khớp** | Cả hai cùng quyết định nền tảng chưa chốt, cùng R9/BR-D5; không mâu thuẫn. |
| 15 | build-mind-map → skill kế tiếp | "Gợi ý dùng tiếp" trỏ build-glossary, plan-requirements-workshop, prepare-stakeholder-interview | **Khớp** | Slug đúng; nội dung gợi ý hợp lý. |

Tóm lại: chuỗi 1–4 dùng được nhưng có **một lệch mã luồng (E3)** và các lệch tên nhỏ; chuỗi 5 (State) chưa được thử; nhánh dữ liệu (8) và nhánh R/BR (10) khớp tốt.

---

## 5. Câu hỏi mở gộp cho trainer (khử trùng lặp, nhóm theo chủ đề)

Nguồn: Câu hỏi mở của 24 output.md và các mâu thuẫn trong case. Mỗi câu ghi người cần trả lời.

**A. Ngưỡng và quy trình chiết khấu**
1. Đầu mút ngưỡng 5% và 10%: case viết "<5%", "5%–10%", ">10%". Hiểu "5%–10%" gồm cả hai đầu (suy ra từ cách viết, các skill đều đang giả định như vậy: AC-07/08, data dictionary, BR-C1). Cần xác nhận chính thức, và ngưỡng đã có văn bản chính sách hay chỉ là thói quen. (Anh Quang, Chị Hạnh) Ghi chú: ở đây thực chất không có mâu thuẫn nếu "5%–10%" gồm hai đầu; chỉ cần ghi vào `_shared` một câu.
2. "Chiết khấu chuẩn" ở UC-01 bước 5 là gì, lấy từ đâu (hạng đại lý, ERP)? Ngưỡng 5%/10% tính trên tổng (chuẩn + xin thêm) hay chỉ phần xin thêm? (Chị Hạnh, Chị Loan, Anh Quang)
3. Chiết khấu dưới 5% tự áp: có đi qua A1 không, có bắt lý do và lưu người áp không? Có trần chiết khấu tối đa không? (Chị Hạnh, Anh Quang)
4. Khi chiết khấu bị từ chối: đơn về trạng thái nào, đại lý được xin lại không và tối đa mấy lần? Sau khi duyệt đơn tự đi tiếp bước 7 hay đại lý gửi lại? Thời hạn duyệt, ai thay khi người duyệt vắng, khi nào leo thang? (Chị Hạnh, Anh Quang)

**B. Công nợ và trạng thái đơn**
5. "Quá hạn công nợ" tính từ mốc nào, "hạng đại lý" gồm những hạng nào? R11 chọn phương án nào (không cho đặt đơn mới, hay giữ đơn và báo Kế toán)? (Chị Loan)
6. Đơn "Chờ kế toán xử lý": giữ ở cổng hay đã ghi ERP (mã đơn ERP có chưa)? Kế toán có những lựa chọn nào (thả, hủy), thời hạn xử lý, ai nhận thông báo (hộp thư chung hay đích danh)? Đại lý có được thấy số công nợ không? Thứ tự khi đơn vừa chờ duyệt chiết khấu vừa quá hạn công nợ? (Chị Loan, Chị Hạnh)
7. F4 cần những trạng thái đơn nào ngoài 4 trạng thái hiện có (đang giao, đã giao, hủy, giao một phần, chiết khấu bị từ chối)? Ngày giao dự kiến lấy từ ERP không? Cần lịch sử đổi trạng thái? Đơn chờ duyệt đã có mã đơn chưa? (Anh Nhân, Chị Hạnh, Chị Loan)
8. Đặt vượt tồn kho (đặt trước) có cho không? Sản phẩm tồn 0 có hiện không? Tồn kho đổi giữa lúc thêm dòng và lúc gửi có kiểm lại không? (Chị Hạnh, Chị Loan)

**C. Số lượng và dữ liệu đại lý**
9. ~200 đại lý ký hợp đồng so với ~300 bản ghi cần import (case nêu cả hai): phần chênh là đại lý ngừng hoạt động, trùng, hay nhóm khác? Sau lọc còn bao nhiêu? (Chị Hạnh)
10. Đại lý trùng xét theo thuộc tính nào? Excel hay ERP là master hồ sơ? Mã đại lý nào là chuẩn? "Đại lý lớn" và "hạng đại lý" có tiêu chí nào? Một đại lý có nhiều tài khoản người dùng không? (Chị Hạnh, Chị Loan, Anh Kiên)

**D. Báo dự án và phân quyền**
11. R9 (sales khu vực xem mọi đại lý, cả vùng khác) so với BR-D5 và nguyên tắc phân quyền theo vùng: sales xem theo vùng hay toàn quốc, chỉ đọc hay được sửa? BR-D5 áp cho vai nào? (Anh Quang, Chị Hạnh, Anh Kiên)
12. Thông báo "bị trùng" được lộ thông tin gì cho đại lý báo sau (đại lý nào, tên dự án)? (Chị Hạnh, Anh Nhân)
13. So khớp "trùng" của BR-D1: tuyệt đối, chuẩn hóa, hay chuẩn hóa kèm cờ nghi trùng? Chủ đầu tư viết tắt ("Cty") xử lý ra sao? (Chị Hạnh)
14. Khoảng trống BR-D2…D4: dự án đang chờ duyệt có được coi là trùng không (R4 muốn báo ngay)? Hết 90 ngày bảo hộ thì sao? Hai đại lý báo cùng dự án khi chưa dự án nào được duyệt: ai ưu tiên (ngày nhận hay ngày duyệt)? Dự án bị từ chối có được báo lại? Bảo hộ là 90 ngày hay "khoảng 3 tháng", mấy lần gia hạn, ngoại lệ cho đại lý lớn? (Chị Hạnh)

**E. Phạm vi, lịch, mục tiêu**
15. F5 Duyệt chiết khấu thuộc Phase 1 hay Phase 2? Case liệt kê Phase 1 gồm đăng ký, báo dự án, đặt hàng và theo dõi đơn, ERP, import, không có F5; Phase 2 chỉ có bảo hành và báo cáo; trong khi UC-01 A1, model-business-process, brainstorming đều coi F5 là Phase 1. (Anh Quang, Chị Hạnh)
16. Mốc thời gian: Phase 1 dài 3 tháng nhưng case nói "còn 3 sprint × 2 tuần, backlog kín" khi nền tảng cổng chưa chốt. Thời điểm thật của dự án là lúc nào, đã xây phần nào? Ngày hội nghị đại lý? (PM, Anh Quang)
17. Change Request F8 (đa ngôn ngữ, đã out of scope) và F9 (SSO cho đại lý): xử lý bằng change request, lùi mốc hay đưa sang Phase 2? R10 (app nhà thầu) ngoài scope nhưng nằm trong danh sách R: ghi nhận ở backlog? (Anh Quang)
18. R1: "4 giờ" tính theo trung bình, trung vị hay % đơn? Mốc bắt đầu là giờ nhận email/Zalo hay giờ nhập? Có tính thời gian chờ duyệt chiết khấu và chờ Kế toán không? 70% đơn qua cổng cần đạt sau bao lâu? (Anh Quang, Chị Hạnh)
19. Nền tảng cổng (web tùy biến hay Salesforce): ai quyết, khi nào, ngân sách và mức ưu tiên giữa chi phí và tốc độ? (Anh Quang, Anh Kiên)

**F. ERP và kỹ thuật**
20. Tài liệu kỹ thuật kết nối ERP khi nào có, ai là đầu mối? ERP cấp mã khách hàng và mã đơn không? Giá và tồn kho truy vấn trực tiếp hay đồng bộ? Đồng bộ hay bất đồng bộ, thời gian chờ, thử lại, chống tạo đơn trùng khi ERP đã nhận nhưng không phản hồi? (Chị Loan, dev)
21. Các exception E3, E4 (BA đề xuất `[GIẢ ĐỊNH]`) có đưa vào Phase 1 không, và E5 (ERP lỗi lúc tải danh mục) có thêm không? (Anh Kiên, Chị Loan, Chị Hạnh)

**G. Phi chức năng**
22. "Mạng yếu" thực tế là gì (3G, 4G chập chờn, vùng nào, thử ở Đà Nẵng được không)? Tải đỉnh cuối tháng: bao nhiêu đại lý/đơn cùng lúc? Mức sẵn sàng 99,5% và chi phí có chấp nhận được? "Vài bước" tối đa bao nhiêu lần chạm? (Anh Nhân, Chị Hạnh, Chị Loan, Anh Quang)
23. Chính sách mật khẩu, thời gian khóa và cách mở khóa; "mọi thao tác duyệt" có gồm xử lý đơn của Kế toán không; thời gian lưu vết (đang giả định 36 tháng)? (Anh Kiên, Chị Loan)

**H. Quyết định nội bộ của trainer**
24. Duyệt bảng "Quy ước mã" (mục 3.4) và BR-C1…C7, BR-P1 (mục 3.3) để đưa vào `_shared`. (Trainer)
25. Khi repo và skill hệ thống (`ba-flow-diagram`, `sf-functional-design-writer`, `designpro`…) trùng cụm kích hoạt thì ưu tiên bên nào? (Trainer)
26. Giữ hay bỏ chi tiết tự thêm "ngưỡng 8%", "ưu tiên theo ngày nhận" trong analyze-source-documents (khuyến nghị: giữ, gắn nhãn, xem mục 7). (Trainer)

---

## 6. Những việc tôi KHÔNG kiểm được hoặc kiểm chưa đủ

1. **Tiêu chí 4 (Ổn định)**: không thể chạy model thật 3 lần. Mọi cột "Ổn định" là đánh giá rủi ro từ độ mơ hồ của SKILL.md. Không có skill nào được ghi "Đạt" ở tiêu chí này.
2. **Kích hoạt**: không có router thật; mọi "đoán kết quả" ở 1A là dự đoán từ chữ. Tôi không biết skill hệ thống (`ba-flow-diagram`, v.v.) hay skill repo thắng khi cùng khớp.
3. **Mermaid**: chỉ kiểm cú pháp bằng `mermaid.parse` (14/14 hợp lệ); chưa render ra SVG nên chưa biết bố cục có đọc được không (ví dụ sơ đồ 32 nút của model-business-process).
4. **SQL của mine-usage-data**: chưa chạy trên PostgreSQL thật. Chỉ tính lại bằng Python logic tương đương. Hành vi `PERCENTILE_CONT` trên cột `numeric`, `ROLLUP` với `ORDER BY ... NULLS LAST`, làm tròn `ROUND` numeric chưa được thử trên engine thật.
5. **So sánh với BABOK v3**: không có bản sách trong tay; chỉ kiểm rằng mục 1 diễn đạt lại, không chép nguyên văn, và có nêu technique. Không đối chiếu từng khái niệm với sách.
6. **Phần references/**: đọc `rule-patterns.md`, `thang-cham-rui-ro.md`, `ai-error-taxonomy.md`, và lướt các file còn lại để lấy slug; chưa đọc kỹ từng dòng của 20+ file reference khác. Lỗi trong references (nếu có) ngoài các chỗ nêu có thể còn sót.
7. **Các "Câu hỏi mở" trong từng output**: tôi kiểm xem có xuất phát từ chỗ thiếu của input không bằng cách đọc, không có quy tắc đo; khử trùng lặp ở mục 5 là thủ công.
8. **Độ phủ của mục "chạy tay"**: với skill thuần văn bản (survey, brainstorming, workshop, SWOT, risks, benchmark) tôi kiểm số học, tính đầy đủ và tuân thủ quy tắc cứng của SKILL.md; không có cách đo "chất lượng" của câu hỏi hay ý tưởng ngoài đối chiếu quy tắc.
9. **Các bản chạy khác của model** có thể sinh lỗi khác lỗi đã liệt kê; báo cáo này chỉ nói về các output.md hiện có.

---

## 7. Quyết định về chi tiết tự thêm của subagent A ("ngưỡng 8%", ưu tiên "Ngày nhận")

**Thực tế đã kiểm.** Hai chi tiết nằm ở `analyze-source-documents/examples/input.md` §6 (dòng 18: ưu tiên đại lý báo trước theo Ngày nhận) và §7 (dòng 20: chiết khấu trên 8% hỏi Giám đốc). Chúng chỉ lặp **một phần** ở build-glossary: input glossary không có "8%" và không có "ưu tiên theo ngày nhận"; nó lặp "khoảng 3 tháng", "đại lý lớn được gia hạn" và "mức nhỏ chị duyệt, mức cao hỏi anh Quang" (Q5–Q10). Chi tiết "3 và 8 và 12 %" xuất hiện lần thứ ba, có chủ ý, trong retro của summarize-lessons-learned (N4, N5) làm "lỗi AI bịa ngưỡng".

**Đánh giá.**
- Giữ được vì analyze-source-documents cần tài liệu có chỗ lệch với case để minh họa "Mâu thuẫn". Đây là nội dung của một tài liệu giả lập đang bị phân tích, không phải khẳng định về case.
- Phần "ưu tiên theo Ngày nhận" thậm chí hữu ích: nó chạm đúng khoảng trống thật của case (G-02(b) của analyze-business-rules và L-05 của pre-review: hai đại lý báo cùng dự án khi chưa dự án nào được duyệt thì ai được ưu tiên).
- Rủi ro: (1) trainer đọc nhầm 8% thành dữ kiện của case; (2) input không ghi nhãn `[GIẢ ĐỊNH]` cho §6, §7, trái `_shared` ("cần thêm chi tiết thì ghi `[GIẢ ĐỊNH]`"); (3) cả bộ ví dụ giờ có ba con số ngưỡng khác nhau (5/10, 8, 3/8/12).

**Khuyến nghị: giữ, nhưng gắn nhãn và không lặp thêm.** Việc sửa tối thiểu:
- `analyze-source-documents/examples/input.md` dòng 6 (tiêu đề tài liệu): thêm "(tài liệu giả lập, §6 và §7 có chủ ý lệch case `[GIẢ ĐỊNH]`)". Không cần đổi §6, §7.
- build-glossary: không cần sửa (không chứa 8% hay Ngày nhận). Nếu muốn tránh "đại lý lớn được gia hạn" là chi tiết thứ hai tự thêm thì ghi Loại "Ý kiến" (đã là "Rule, Ý kiến").

**Nếu trainer chọn bỏ**, sửa đúng các dòng sau (đã kiểm số dòng):
- input.md: xóa §6 (dòng 18) và §7 (dòng 20); đánh số lại §8–§10 hoặc để trống.
- output.md: bỏ RT-06 (dòng 15), RT-07 (dòng 16), RT-09 (dòng 18); bỏ ý "Ngày nhận" ở bảng Thuật ngữ (dòng 29, dòng "Ngày nhận / Ngày duyệt" chỉ còn "hai mốc ngày"); bỏ G1 (dòng 35), G3 (dòng 37); sửa G2 (dòng 36) thành "Đại lý lớn có ngoại lệ ngầm ở §5"; sửa Tóm tắt (dòng 5) bỏ "§6" và câu cuối về chiết khấu (§7); bỏ Câu hỏi mở 1 và 3 (dòng 45, 47) và đánh số lại. Khi đó skill mất hai ví dụ "Mâu thuẫn" rõ nhất và chỉ còn RT-04 "≈" và G2.
- Cập nhật con số: "9 RT" thành 6, "8 G" thành 6, "7 câu hỏi" thành 5.
