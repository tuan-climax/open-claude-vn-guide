# Marketing Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.

---

## MKT-01: Content Repurposing (1 bài → 4 format)

```
<role>Digital Marketing Manager, thành thạo multi-channel content strategy</role>

<instructions>
Từ bài viết gốc dưới đây, tạo 4 format:
1. LinkedIn post (150-250 từ, hook mạnh + 3-5 insights + CTA)
2. Twitter/X thread (5-6 tweets, mỗi tweet 1 insight)
3. Email newsletter snippet (subject line + 100-150 từ + CTA)
4. Slide deck outline (title + 3-4 slides + conclusion)

Giữ nguyên tất cả số liệu từ bài gốc — không thêm số không có.
</instructions>

<brand_context>
Tone: [chuyên nghiệp / thân thiện / data-driven / ...]
Audience: [target của bạn]
Tránh: [buzzwords bạn không muốn dùng]
</brand_context>

<original_content>
[Paste bài blog/article gốc]
</original_content>
```

---

## MKT-02: Social Media Copy (A/B variations)

```
<role>Social Media Copywriter, thành thạo B2B content</role>

<instructions>
Viết 3 variations của post cho [LinkedIn / Facebook / Twitter]:
- Variation A: Hook là câu hỏi kích thích
- Variation B: Hook là số liệu bất ngờ
- Variation C: Hook là câu chuyện/anecdote ngắn

Mỗi variation: 150-200 từ + 2-3 hashtag + 1 CTA rõ ràng.
Sau đó đề xuất: Variation nào phù hợp nhất cho audience [B2B/B2C] và tại sao?
</instructions>

<content_brief>
Topic: [chủ đề]
Key message: [thông điệp chính muốn truyền]
Target audience: [mô tả audience]
Goal: [awareness / engagement / leads / ...]
CTA muốn: [link / DM / comment / ...]
</content_brief>
```

---

## MKT-03: Campaign Brief

```
<role>Marketing Strategist, chuyên lập kế hoạch campaign B2B/B2C</role>

<instructions>
Tạo campaign brief chi tiết gồm:
1. Campaign overview (objective, target, timeline)
2. Target audience profile (demographics, pain points, motivations)
3. Key messages (1 primary + 2-3 supporting)
4. Channel mix (kênh nào, tần suất, budget allocation)
5. Content calendar (4 tuần, mỗi tuần 3-5 posts)
6. KPIs và cách đo lường
</instructions>

<campaign_input>
Sản phẩm/dịch vụ: [Tên]
Mục tiêu: [Leads / Brand awareness / Retention / ...]
Target: [Mô tả khách hàng mục tiêu]
Budget: [Range nếu có]
Timeline: [Bắt đầu → kết thúc]
Competitor landscape: [Đối thủ đang làm gì]
</campaign_input>
```

---

## MKT-04: Competitor Analysis

```
<role>Market Research Analyst, thành thạo competitive intelligence</role>

<instructions>
Phân tích đối thủ cạnh tranh dựa trên thông tin dưới đây:
1. So sánh positioning (bảng 2x2: value prop + target)
2. Điểm mạnh của từng đối thủ
3. Điểm yếu / gaps của từng đối thủ
4. Opportunity gaps cho mình có thể khai thác
5. 3 khuyến nghị điều chỉnh strategy

Chỉ dùng thông tin trong <competitor_data> — không bịa.
</instructions>

<competitor_data>
Công ty A: [website, tagline, pricing nếu biết, key features]
Công ty B: [tương tự]
Công ty C: [tương tự]

Mình: [tên, positioning hiện tại]
</competitor_data>
```

---

## MKT-05: Email Marketing Sequence

```
<role>Email Marketing Specialist, thành thạo nurture sequences</role>

<instructions>
Viết email sequence 5 bước cho [lead mới / trial users / churn risk]:
- Email 1 (Day 0): Welcome + value ngay lập tức
- Email 2 (Day 3): Giáo dục — giải quyết pain point #1
- Email 3 (Day 7): Social proof / case study
- Email 4 (Day 14): Feature highlight phù hợp nhất với segment
- Email 5 (Day 21): CTA mạnh — upgrade / demo / renew

Mỗi email: subject line + preview text + body (150-200 từ) + CTA.
</instructions>

<context>
Sản phẩm: [Tên sản phẩm]
Segment: [loại user/lead này là ai]
Pain points chính: [1-2 pain points]
CTA cuối sequence: [Mục tiêu conversion]
</context>
```
