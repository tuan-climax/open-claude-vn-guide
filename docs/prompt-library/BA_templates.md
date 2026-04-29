# BA/Product Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.

---

## BA-01: Research Synthesis từ Transcripts

```
<role>Senior Business Analyst, chuyên phân tích qualitative research</role>

<instructions>
Tổng hợp các transcript interview dưới đây:
1. Xác định top 5 pain points (tần suất + severity)
2. Nhóm thành 3-4 themes chính
3. Quote tiêu biểu cho mỗi theme (1-2 câu nguyên văn)
4. Đề xuất 3-5 feature ưu tiên dựa trên impact × frequency
5. Priority matrix: P0 / P1 / P2

Chỉ dùng thông tin từ <transcripts> — không suy đoán.
Quote phải là nguyên văn — không paraphrase.
</instructions>

<transcripts>
[Paste transcript interviews / feedback / survey responses]
</transcripts>

<output_format>
## Research Synthesis Report
Nguồn: [N] transcripts | Ngày: [date]

### Pain Points (Top 5)
| # | Pain | Tần suất | Severity |
|---|------|----------|----------|

### Themes
#### Theme 1: [Tên]
Mô tả: [1-2 câu]
Quote: "[nguyên văn]"

### Feature Opportunities & Priority Matrix
</output_format>
```

---

## BA-02: User Story từ Meeting Notes

```
<role>Business Analyst, viết user stories chuẩn Agile</role>

<instructions>
Từ ghi chú cuộc họp dưới đây, viết user stories:
1. Format: "Là [persona], tôi muốn [action] để [benefit]"
2. Acceptance Criteria (3-5 AC mỗi story, có thể đo được)
3. Out of scope (điều explicitly không làm trong story này)
4. Dependencies (story nào phải xong trước)
5. Story points estimate (1/2/3/5/8 — nếu đủ thông tin)

Mỗi AC phải đo được — không dùng "nhanh", "đẹp", "tốt".
</instructions>

<meeting_notes>
[Paste ghi chú từ meeting với stakeholder]
</meeting_notes>
```

---

## BA-03: PRD Draft từ Brief

```
<role>Senior Product Manager, viết PRD rõ ràng và actionable</role>

<instructions>
Từ brief dưới đây, viết Product Requirements Document (PRD):
1. Overview: problem statement, success metrics, timeline
2. User personas (2-3 personas với pain points)
3. User journeys (happy path cho mỗi persona)
4. Functional requirements (must-have vs nice-to-have)
5. Non-functional requirements (performance, security, scalability)
6. Out of scope (explicit)
7. Open questions (cần quyết định trước khi build)
</instructions>

<brief>
Feature/Product: [Tên]
Problem: [Vấn đề đang giải quyết]
Target users: [Ai sẽ dùng]
Success metrics: [Đo thành công thế nào]
Timeline: [Deadline]
Constraints: [Giới hạn kỹ thuật / business / resource]
</brief>
```

---

## BA-04: Stakeholder Interview Prep

```
<role>Business Analyst, chuẩn bị interview với stakeholders</role>

<instructions>
Chuẩn bị bộ câu hỏi phỏng vấn stakeholder cho:
1. Group A — Discovery (4-5 câu): hiểu pain points hiện tại
2. Group B — Requirements (4-5 câu): clarify expectations
3. Group C — Constraints (3 câu): budget, timeline, technical limits
4. Group D — Success criteria (2-3 câu): định nghĩa thành công

Mỗi câu: open-ended, không leading.
Sau interview guide: gợi ý cách capture notes và next steps.
</instructions>

<context>
Project/Feature: [Tên]
Stakeholder: [Tên và role]
Meeting duration: [N phút]
Điều đã biết: [Thông tin background]
Điều cần làm rõ: [Những gì còn unclear]
</context>
```

---

## BA-05: Gap Analysis

```
<role>Business Analyst, phân tích khoảng cách giữa hiện tại và mục tiêu</role>

<instructions>
Phân tích gap giữa current state và desired state:
1. Current state: mô tả quy trình/hệ thống hiện tại
2. Desired state: mô tả mục tiêu cần đạt
3. Gaps identified: những gì còn thiếu/cần thay đổi
4. Root causes: tại sao gaps tồn tại
5. Recommendations: 3-5 bước để bridge the gap
6. Priority: gap nào cần xử lý trước

Format: bảng comparison + narrative cho mỗi gap.
</instructions>

<current_state>
[Mô tả hiện trạng: quy trình, tools, con người, data]
</current_state>

<desired_state>
[Mô tả trạng thái mong muốn sau khi implement]
</desired_state>
```
