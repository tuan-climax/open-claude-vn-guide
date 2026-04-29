# Dev Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.
Với Dev, nên dùng Claude Code CLI (`claude` trong terminal) để có đầy đủ file access.

---

## DEV-01: Code Review

```
<role>Senior Software Engineer, reviewer nghiêm khắc và constructive</role>

<instructions>
Review code dưới đây theo 4 chiều (ưu tiên thứ tự):
1. Security: SQL injection, auth bypass, hardcoded secrets, sensitive data exposure
2. Logic: edge cases, NULL handling, error handling, race conditions
3. Performance: N+1 queries, memory leaks, expensive hot path
4. Style: naming clarity, DRY, type hints, comment WHY not WHAT

Phân loại mỗi issue:
🔴 PHẢI SỬA (block merge)
🟡 NÊN SỬA (recommend)
💡 GỢI Ý (optional)

Kèm code suggestion cụ thể cho mỗi 🔴 issue.
Khen những gì làm tốt — review cân bằng.
</instructions>

<code_to_review>
[Paste code cần review]
</code_to_review>

<context>
Language: [Python / JavaScript / Go / ...]
Framework: [FastAPI / Express / ...]
Coding conventions: [xem coding-conventions.md hoặc mô tả ngắn]
</context>
```

---

## DEV-02: Test Plan Generation

```
<role>QA Engineer, viết test cases toàn diện</role>

<instructions>
Viết test plan cho feature dưới đây:
1. Unit tests: mỗi function/method chính + edge cases
2. Integration tests: component interactions
3. E2E tests: happy path + critical user journeys
4. Negative tests: invalid inputs, error states
5. Performance tests (nếu cần): load, response time thresholds

Với mỗi test case: description + input + expected output + priority (P0/P1/P2)
</instructions>

<feature>
[Mô tả feature hoặc paste code cần test]
</feature>

<acceptance_criteria>
[AC từ user story — test phải verify được tất cả AC này]
</acceptance_criteria>
```

---

## DEV-03: Debug với Log Analysis

```
<role>Senior Engineer, chuyên debugging production issues</role>

<instructions>
Phân tích error log dưới đây:
1. Root cause (không phải symptom — đi đến nguyên nhân gốc)
2. Error chain: chuỗi sự kiện dẫn đến lỗi
3. Affected scope: những gì có thể bị ảnh hưởng
4. Fix đề xuất (code change cụ thể)
5. Prevention: làm gì để không tái diễn

Format: bullet points, kỹ thuật, không vòng vo.
</instructions>

<error_log>
[Paste error log / stack trace]
</error_log>

<context>
Service: [tên service]
Language/Framework: [...]
Khi nào xảy ra: [điều kiện trigger]
Đã thử: [những gì đã làm để debug]
</context>
```

---

## DEV-04: Refactoring Plan

```
<role>Senior Software Engineer, chuyên code quality và refactoring</role>

<instructions>
Phân tích code dưới đây và tạo refactoring plan:
1. Code smells hiện tại (list với mức severity)
2. Refactoring goals (đạt được gì sau khi refactor)
3. Step-by-step plan (chia nhỏ, mỗi step an toàn, có thể test riêng)
4. Risk assessment (gì có thể break, cần test gì trước)
5. Estimated effort (số giờ ước tính)

QUAN TRỌNG: Chỉ lập kế hoạch — KHÔNG tự refactor cho đến khi plan được approve.
</instructions>

<code>
[Paste code cần refactor]
</code>

<context>
Lý do refactor: [Performance / Maintainability / Onboarding / Tech debt]
Constraints: [Timeline, không được break API, ...]
Test coverage hiện tại: [% nếu biết]
</context>
```

---

## DEV-05: API Documentation

```
<role>Technical Writer / Developer, viết API docs cho developers</role>

<instructions>
Viết documentation cho API endpoints dưới đây:
1. Overview: mục đích endpoint, authentication required
2. Request: method, URL, headers, body parameters (type + required + description)
3. Response: status codes, response schema, examples
4. Error codes: mỗi error code + meaning + common causes
5. Code examples: curl + [language của bạn]
6. Rate limits (nếu có)
</instructions>

<api_code>
[Paste API endpoint code hoặc describe endpoints]
</api_code>

<output_format>
## [Endpoint name]

**`[METHOD] /api/v1/path`**

[Mô tả ngắn]

### Request
```http
Headers, body...
```

### Response
```json
{...}
```

### Examples
```curl
...
```
</output_format>
```
