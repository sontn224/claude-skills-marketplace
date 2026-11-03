# Checklist chất lượng skill

Chấm từng skill theo 5 tiêu chí. Mỗi tiêu chí ghi **Đạt / Chưa đạt** kèm lý do một dòng.

## 1. Kích hoạt đúng
- Viết 3 prompt **nên** kích hoạt skill và 3 prompt **không nên** (đáng lẽ thuộc skill khác).
- Đọc `description` rồi tự trả lời: skill có được chọn không?
- **Đạt** khi đúng ít nhất 5/6.
- `description` phải có: skill làm gì, khi nào dùng, khi nào không dùng, 2–3 cụm kích hoạt tiếng Việt.

## 2. Đúng format
- Có đủ 8 mục theo `_template/SKILL.md`, đúng thứ tự, đúng tên mục.
- Frontmatter có `name` (đúng slug trong plan) và `description`.
- Mẫu đầu ra là bảng hoặc khung cố định; sơ đồ dùng Mermaid và render được (cú pháp hợp lệ).
- SKILL.md tối đa khoảng 150 dòng; phần dài nằm trong `references/`.
- Có `examples/input.md` và `examples/output.md`; output khớp đúng mẫu ở mục 4.

## 3. Đúng nội dung
- Bám technique trong BABOK v3, không chép nguyên văn sách.
- Không bịa rule: mọi rule, số liệu, tên không có nguồn trong input đều gắn `[GIẢ ĐỊNH]`.
- Có nhánh lỗi và nhánh biên nếu technique cần (use case, AC, sequence, state, process).
- Ví dụ dùng đúng dữ kiện trong `_shared/case-dai-viet-electric.md`, không mâu thuẫn với case.
- Kết thúc bằng mục "Câu hỏi mở", và câu hỏi thật sự xuất phát từ chỗ thiếu của input.

## 4. Ổn định
- Chạy skill 3 lần với cùng `examples/input.md`.
- **Đạt** khi cấu trúc, số mục, kết luận chính giống nhau; chỉ khác cách diễn đạt.
- Ghi lại chỗ khác nhau đáng kể (ví dụ lần 1 có 3 exception, lần 2 có 1).

## 5. An toàn dữ liệu
- Không có tên người, số điện thoại, email, giá, hợp đồng, công nợ thật.
- Ví dụ chỉ dùng case hư cấu Đại Việt Electric.
- Mục 7 trong SKILL.md có nhắc ẩn danh và nhãn `[GIẢ ĐỊNH]`.

## Bảng chấm

| Skill | Kích hoạt | Format | Nội dung | Ổn định | Dữ liệu | Kết luận | Lỗi và đề xuất sửa |
|---|---|---|---|---|---|---|---|

## Tính nhất quán giữa các skill (dành cho reviewer)
- Cùng giọng văn (tiếng Việt, câu ngắn, thuật ngữ BABOK giữ tiếng Anh), cùng tên 8 mục.
- Chuỗi nối tiếp dùng được đầu ra của nhau: Interviews → Glossary → Use Case → User Story/AC → Sequence/State.
- Mã định danh dùng thống nhất (UC-01, BR-D1, R1–R12, F1–F9) theo `_shared/case-dai-viet-electric.md`.
