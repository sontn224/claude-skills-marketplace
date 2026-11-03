# ba-skills — Agent Skill cho các technique có nhãn AI trên BA Skill Map

> Cập nhật lần cuối: 2026-11-03. Trạng thái: **bản nháp (v0.1.0)**, chưa kiểm tiêu chí "Ổn định".
> Nguồn kế hoạch: `30_AI/ba-skill-map-skills-plan.md`. Ví dụ dùng case hư cấu Đại Việt Electric (`_shared/case-dai-viet-electric.md`).

24 skill cho 25 technique (User Stories và Acceptance Criteria dùng chung một skill). Mỗi skill có `SKILL.md` (8 mục theo `_template/SKILL.md`), `examples/input.md`, `examples/output.md`, và thường có `references/`.

## Index

| # | Slug | Technique BABOK v3 | Knowledge area | Node id | Trạng thái |
|---|---|---|---|---|---|
| 1 | [prepare-stakeholder-interview](skills/prepare-stakeholder-interview/SKILL.md) | Interviews | 1 · Elicitation & Collaboration | ec-0 | Viết mới, đã review 1 vòng |
| 2 | [plan-requirements-workshop](skills/plan-requirements-workshop/SKILL.md) | Workshops | 1 · Elicitation & Collaboration | ec-1 | Đã review 1 vòng |
| 3 | [design-survey-and-analyze](skills/design-survey-and-analyze/SKILL.md) | Survey or Questionnaire | 1 · Elicitation & Collaboration | ec-3 | Đã review 1 vòng |
| 4 | [analyze-source-documents](skills/analyze-source-documents/SKILL.md) | Document Analysis | 1 · Elicitation & Collaboration | ec-5 | Đã review 1 vòng |
| 5 | [facilitate-brainstorming](skills/facilitate-brainstorming/SKILL.md) | Brainstorming | 1 · Elicitation & Collaboration | ec-6 | Đã review 1 vòng |
| 6 | [build-mind-map](skills/build-mind-map/SKILL.md) | Mind Mapping | 1 · Elicitation & Collaboration | ec-8 | Đã review 1 vòng |
| 7 | [build-glossary](skills/build-glossary/SKILL.md) | Glossary | 1 · Elicitation & Collaboration | ec-9 | Đã review 1 vòng |
| 8 | [model-business-process](skills/model-business-process/SKILL.md) | Process Modelling | 2 · Requirements Analysis & Design Definition | radd-1 | Đã review 1 vòng |
| 9 | [write-use-case-spec](skills/write-use-case-spec/SKILL.md) | Use Cases and Scenarios | 2 · Requirements Analysis & Design Definition | radd-2 | Viết mới, đã review 1 vòng |
| 10 | [draw-sequence-diagram](skills/draw-sequence-diagram/SKILL.md) | Sequence Diagrams | 2 · Requirements Analysis & Design Definition | radd-10 | Đã review 1 vòng |
| 11 | [draw-state-diagram](skills/draw-state-diagram/SKILL.md) | State Modelling | 2 · Requirements Analysis & Design Definition | radd-11 | Đã review 1 vòng |
| 12 | [write-user-story-and-ac](skills/write-user-story-and-ac/SKILL.md) | User Stories + Acceptance and Evaluation Criteria | 2 · Requirements Analysis & Design Definition | radd-3, radd-4 | Viết mới, đã review 1 vòng |
| 13 | [generate-prototype-screens](skills/generate-prototype-screens/SKILL.md) | Prototyping | 2 · Requirements Analysis & Design Definition | radd-5 | Đã review 1 vòng |
| 14 | [draft-data-model](skills/draft-data-model/SKILL.md) | Data Modelling | 2 · Requirements Analysis & Design Definition | radd-6 | Đã review 1 vòng |
| 15 | [build-data-dictionary](skills/build-data-dictionary/SKILL.md) | Data Dictionary | 2 · Requirements Analysis & Design Definition | radd-7 | Đã review 1 vòng |
| 16 | [write-nfr](skills/write-nfr/SKILL.md) | Non-Functional Requirements Analysis | 2 · Requirements Analysis & Design Definition | radd-13 | Đã review 1 vòng |
| 17 | [pre-review-requirements](skills/pre-review-requirements/SKILL.md) | Reviews | 3 · Requirements Life Cycle Management | rlcm-2 | Đã review 1 vòng |
| 18 | [analyze-business-rules](skills/analyze-business-rules/SKILL.md) | Business Rules Analysis | 3 · Requirements Life Cycle Management | rlcm-4 | Đã review 1 vòng |
| 19 | [draft-swot](skills/draft-swot/SKILL.md) | SWOT Analysis | 4 · Strategy Analysis | sa-1 | Đã review 1 vòng |
| 20 | [research-benchmark](skills/research-benchmark/SKILL.md) | Benchmarking and Market Analysis | 4 · Strategy Analysis | sa-4 | Đã review 1 vòng (reviewer không tìm thấy lỗi) |
| 21 | [identify-risks](skills/identify-risks/SKILL.md) | Risk Analysis and Management | 4 · Strategy Analysis | sa-6 | Đã review 1 vòng |
| 22 | [summarize-lessons-learned](skills/summarize-lessons-learned/SKILL.md) | Lessons Learned | 5 · Planning (Lessons Learned) | pm-3 | Đã review 1 vòng |
| 23 | [analyze-root-cause](skills/analyze-root-cause/SKILL.md) | Root Cause Analysis | 6 · Solution Evaluation | se-1 | Đã review 1 vòng |
| 24 | [mine-usage-data](skills/mine-usage-data/SKILL.md) | Data Mining | 6 · Solution Evaluation | se-2 | Đã review 1 vòng, số liệu SQL đã tính lại |

Cột "Trạng thái" nghĩa là: đã qua tự chấm của người viết, 1 vòng review chéo bởi reviewer độc lập, và 1 vòng sửa. **Chưa skill nào kiểm tiêu chí "Ổn định"** (chạy 3 lần cùng input), nên chưa skill nào được coi là "Đạt" theo checklist.

## Chuỗi nối tiếp

```
prepare-stakeholder-interview → build-glossary → write-use-case-spec → write-user-story-and-ac → draw-sequence-diagram / draw-state-diagram
draft-data-model → build-data-dictionary
mine-usage-data → analyze-root-cause → identify-risks / summarize-lessons-learned
```

## Cấu trúc

```
plugins/ba-skills/
  .claude-plugin/plugin.json
  README.md
  skills/<slug>/        SKILL.md, examples/, references/   (24 skill, xếp phẳng; knowledge area ghi trong bảng trên)
  _template/SKILL.md            mẫu 8 mục
  _checklist/skill-quality.md   5 tiêu chí review
  _shared/case-dai-viet-electric.md   dữ kiện case, mã BR-C/BR-P, E3–E5, quy ước mã, nhãn nguồn
  _review/review-report.md      báo cáo review chéo vòng 1
```

Đường dẫn `_shared/...` trong các ví dụ tính từ thư mục `plugins/ba-skills/`.

## Ghi chú

- 4 skill của khóa (`prepare-stakeholder-interview`, `classify-requirements`, `write-use-case-spec`, `write-user-story-and-ac`) **chưa có file nào trên máy** khi bắt đầu, nên 3 skill được viết mới theo template. `classify-requirements` không gắn technique nào trên map và chưa được tạo; thêm vào `02-radd/` khi có bản gốc.
- Mã `BR-C1…C7`, `BR-P1`, `E3…E5` là mã do repo đặt, không có trong case gốc.
- Node id lấy từ plan; chưa đối chiếu lại với bản BA Skill Map gốc.
