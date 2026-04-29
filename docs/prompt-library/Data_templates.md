# Data Team Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.

---

## DATA-01: SQL từ câu hỏi Business

```
<role>Data Analyst senior, thành thạo [PostgreSQL / BigQuery / MySQL]</role>

<instructions>
Viết SQL query để trả lời câu hỏi business dưới đây.
Yêu cầu:
- Query tối ưu (dùng CTE nếu phức tạp, tránh subquery lồng nhau)
- Comment giải thích logic từng bước
- Xử lý NULL values rõ ràng
- Ghi chú index nào nên có nếu query chậm
</instructions>

<schema>
[Paste DDL hoặc mô tả schema các bảng liên quan]
Table 1: [tên] ([columns])
Table 2: [tên] ([columns])
</schema>

<question>
[Câu hỏi business, vd: "Tỷ lệ khách hàng churn theo tháng Q1-Q3, phân theo segment?"]
</question>

<output_format>
-- Query
[SQL code]

-- Giải thích
[Mô tả logic từng bước]

-- Ví dụ output mẫu
[Table header với vài dòng data giả]
</output_format>
```

---

## DATA-02: Data Quality Check

```
<role>Data Engineer senior, thành thạo SQL và Python pandas</role>

<instructions>
Kiểm tra chất lượng dataset dưới đây theo 5 chiều:
1. Completeness: NULL rate cho mỗi column quan trọng
2. Uniqueness: Duplicate records theo primary key
3. Validity: Giá trị có trong range hợp lệ không
4. Consistency: Logical rules có đúng không
5. Freshness: Last update so với expected frequency

Với mỗi issue tìm thấy:
- Severity: CRITICAL / HIGH / MEDIUM / LOW
- Số records bị ảnh hưởng + %
- Query SQL để verify
- Đề xuất fix cụ thể
</instructions>

<dataset_info>
Table: [tên bảng]
Records: [N]
Date range: [từ ... đến ...]
Primary key: [column(s)]
Critical columns: [columns quan trọng nhất]
Business rules: [vd: amount > 0, status in ('active','inactive')]
</dataset_info>
```

---

## DATA-03: Dashboard Documentation

```
<role>Data Analyst, tạo documentation cho business dashboards</role>

<instructions>
Tạo documentation cho dashboard dưới đây gồm:
1. Overview: mục đích + audience + refresh frequency
2. Metric definitions: mỗi metric có formula + business meaning
3. Filters & dimensions: giải thích mỗi filter
4. Data lineage: nguồn data và transformation
5. Known limitations: những gì dashboard KHÔNG thể đo
6. FAQ: 5 câu hỏi thường gặp về dashboard này
</instructions>

<dashboard_info>
Tên dashboard: [Tên]
Audience: [Ai dùng]
Metrics chính: [List metrics]
Data sources: [Bảng/nguồn data]
Refresh: [Hàng ngày / Realtime / ...]
</dashboard_info>
```

---

## DATA-04: Anomaly Detection Report

```
<role>Data Analyst, chuyên phát hiện bất thường trong data</role>

<instructions>
Phân tích data dưới đây và phát hiện bất thường:
1. Statistical outliers (ngoài mean ± 2σ)
2. Unexpected spikes/drops (> 30% thay đổi so với ngày/tuần trước)
3. Missing data windows (gaps không giải thích được)
4. Pattern breaks (trend đột ngột thay đổi)

Với mỗi anomaly:
- Mô tả cụ thể (khi nào, metric nào, magnitude)
- Possible causes (2-3 hypothesis)
- Action recommended

Chỉ report facts từ data — không kết luận nguyên nhân chắc chắn.
</instructions>

<data>
[Paste time-series data hoặc metrics cần check]
</data>
```

---

## DATA-05: ETL Pipeline Design

```
<role>Data Engineer, thiết kế data pipelines đáng tin cậy</role>

<instructions>
Thiết kế ETL pipeline cho yêu cầu dưới đây:
1. Source → Staging: extract và validate
2. Staging → Cleaned: transform và standardize
3. Cleaned → Mart: aggregate và business logic
4. Error handling: retry logic, dead letter queue
5. Monitoring: checks cần có ở mỗi bước
6. Schedule và dependencies

Output: step-by-step design với pseudocode cho transformation phức tạp.
</instructions>

<requirements>
Nguồn data: [API / Database / File / ...]
Destination: [Data warehouse / Database / ...]
Frequency: [Realtime / Hourly / Daily / ...]
Data volume: [N records/run ước tính]
Business rules cần apply: [List transformations]
SLA: [Data phải available lúc mấy giờ]
</requirements>
```
