# Data Conventions
<!-- Điều chỉnh theo database/platform thực tế của công ty bạn -->

## SQL Naming

### Tables
- snake_case, số nhiều: `orders`, `user_profiles`, `monthly_reports`
- Prefix theo domain (tuỳ chọn): `mkt_` (marketing), `fin_` (finance), `ref_` (reference/lookup)
- Ví dụ: `mkt_campaigns`, `fin_invoices`, `ref_product_categories`

### Columns
- snake_case, mô tả rõ ràng: `created_at` (không phải `ca` hay `create`)
- Dates: suffix `_at` hoặc `_date` — `created_at`, `report_date`, `closed_at`
- Amounts: suffix `_amount` hoặc currency suffix — `revenue_vnd`, `cost_amount`
- Flags/booleans: prefix `is_` hoặc `has_` — `is_active`, `has_paid`
- IDs: suffix `_id` — `user_id`, `order_id`, `product_id`
- Rates/percentages: suffix `_pct` hoặc `_rate` — `growth_rate`, `margin_pct`

## Project/Schema Structure
<!-- Điều chỉnh theo database/cloud platform của bạn -->
```
[your-project]/
├── raw/        ← dữ liệu thô từ source, KHÔNG modify
├── staging/    ← cleaned, typed, validated
├── marts/      ← business-ready, dùng cho dashboard & API
└── analytics/  ← ad-hoc analysis, có thể xóa
```

## SQL Style Guide

```sql
-- Keywords: UPPERCASE
-- Identifiers: lowercase snake_case
-- Indentation: 2 spaces
-- Aliases: mô tả rõ, không dùng a, b, c

SELECT
  u.user_id,
  u.email,
  o.order_date,
  o.total_amount,
  ROUND(o.total_amount / LAG(o.total_amount) OVER (
    PARTITION BY u.user_id ORDER BY o.order_date
  ) - 1, 4) AS growth_pct
FROM
  users AS u
  INNER JOIN orders AS o ON u.user_id = o.user_id
WHERE
  o.order_date >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
  AND u.is_active = TRUE
ORDER BY
  u.user_id, o.order_date
```

## Data Quality Rules
- NULL handling: luôn explicit — `COALESCE(col, 0)` hoặc filter `WHERE col IS NOT NULL`
- Date range: luôn validate `start_date <= end_date`
- Amounts: không âm nếu không có lý do (flag bất thường)
- Duplicates: check `COUNT(*) vs COUNT(DISTINCT key)` trước khi join
- Joins: dùng INNER/LEFT JOIN explicit, tránh implicit cross join

## Python Data Standards
- DataFrame columns: snake_case, consistent với SQL naming
- Dates: luôn dùng `pd.Timestamp` hoặc `datetime.date`, không dùng string
- Float precision: `round(val, 4)` cho percentages, `round(val, 2)` cho tiền tệ
- Missing values: document explicitly trong function docstring
