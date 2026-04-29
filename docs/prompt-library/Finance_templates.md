# Finance Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.
**Lưu ý**: Mọi output liên quan tài chính cần human review trước khi dùng chính thức.

---

## FIN-01: Variance Analysis (Phân tích chênh lệch)

```
<role>Financial Controller, báo cáo theo VAS, ưu tiên accuracy tuyệt đối</role>

<instructions>
Phân tích bảng chi phí/doanh thu dưới đây:
1. Liệt kê 5 danh mục lớn nhất (Actual vs Budget)
2. Flag TẤT CẢ biến động > 15% so với kỳ trước hoặc budget
3. Với mỗi flag: đề xuất 2 nguyên nhân có thể
4. Đề xuất 3 hành động cụ thể với ước tính tiết kiệm

NGUYÊN TẮC: CHỈ dùng số liệu trong <data>.
Mỗi nhận định phải kèm [Nguồn: dòng X].
Đánh dấu [⚠️ CẦN KIỂM CHỨNG] nếu không chắc.
</instructions>

<data>
[Paste bảng chi phí / doanh thu — CSV hoặc table]
</data>

<output_format>
⚠️ DRAFT — Cần human review trước khi dùng chính thức

## EXECUTIVE SUMMARY
[5 dòng key metrics]

## VARIANCE DETAIL
[Bảng với flag]

## FLAGS VÀ PHÂN TÍCH
[Chi tiết từng flag]

## ĐỀ XUẤT HÀNH ĐỘNG
[3 actions có timeline]
</output_format>
```

---

## FIN-02: Budget vs Actual Report

```
<role>Management Accountant, chuyên reporting nội bộ</role>

<instructions>
Tạo báo cáo Budget vs Actual cho kỳ [tháng/quý]:
1. Tổng quan: Revenue, Expenses, Net (so sánh budget vs actual)
2. Top 5 overspend items + lý do
3. Top 5 underspend items + lý do
4. Forecast điều chỉnh cho kỳ tiếp theo
5. 3 khuyến nghị để cải thiện budget accuracy

Chỉ dùng data trong <financial_data>.
</instructions>

<financial_data>
[Paste data thực tế — có thể là export từ accounting system]
</financial_data>

<constraints>
- Không kết luận nguyên nhân nếu không có evidence — chỉ hypothesis
- Với số liệu quan trọng: ghi rõ nguồn
- Output là draft — cần review trước khi share
</constraints>
```

---

## FIN-03: Reconciliation Check

```
<role>Financial Accountant, thành thạo đối soát sổ sách</role>

<instructions>
Đối soát 2 nguồn số liệu dưới đây:
1. Tìm differences (items có trong A không có trong B và ngược lại)
2. Tìm amount mismatches (cùng item nhưng số khác nhau)
3. Phân loại: Timing difference / Error / Missing entry
4. Đề xuất điều chỉnh cho từng difference
5. Tổng hợp: tổng chênh lệch, số items cần xử lý

KHÔNG tự sửa số liệu — chỉ report và recommend.
</instructions>

<source_a>
[Nguồn A: Accounting system / Bank statement / ...]
</source_a>

<source_b>
[Nguồn B: Internal records / ERP / ...]
</source_b>
```

---

## FIN-04: Expense Report Summary

```
<role>Finance Analyst, tổng hợp và phân tích expense reports</role>

<instructions>
Tổng hợp expense reports dưới đây:
1. Tổng chi phí theo category (table)
2. Flagged items: > [N triệu] hoặc thiếu receipt/approval
3. Pending reimbursements
4. So sánh với tháng trước (nếu có data)
5. Nhận xét bất thường (nếu có)
</instructions>

<expenses>
[Paste data expense reports — CSV hoặc table]
</expenses>

<policy>
[Paste đoạn expense policy liên quan nếu cần check compliance]
</policy>
```

---

## FIN-05: Cash Flow Projection

```
<role>Financial Planning Analyst, thành thạo cash flow modeling</role>

<instructions>
Dựa trên data dưới đây, tạo cash flow projection cho [N tháng tới]:
1. Opening balance mỗi tháng
2. Cash inflows (theo category)
3. Cash outflows (theo category)
4. Closing balance và cumulative cash position
5. Tháng nào có risk cash shortfall → alert + đề xuất mitigation
6. 2 scenarios: Base case và Conservative case

NGUYÊN TẮC: Chỉ dùng data được cung cấp. Ghi rõ assumptions.
</instructions>

<current_data>
[Current cash balance, receivables schedule, payables schedule, known commitments]
</current_data>

<assumptions>
Revenue growth rate: [X%]
Payment terms: [AR N days, AP N days]
Planned investments: [Nếu có]
</assumptions>
```
