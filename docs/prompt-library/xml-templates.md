# XML Prompt Templates
<!-- v1.0 | 2026-04-29 -->

Tổng hợp các XML tag templates hay dùng nhất. Copy → điền vào `[...]` → dùng ngay.

---

## TEMPLATE 1: Cơ bản (4 tag)

```
<role>[Chuyên gia gì — ngắn gọn, cụ thể]</role>

<instructions>
[Mô tả task — dùng số thứ tự nếu nhiều bước]
1. [Bước 1]
2. [Bước 2]
3. [Bước 3]
</instructions>

<data>
[Dán dữ liệu vào đây]
</data>

<output_format>
[Mô tả format: bảng, bullet, markdown, ...]
</output_format>
```

---

## TEMPLATE 2: Đầy đủ (6 tag — khuyến nghị cho task phức tạp)

```
<role>
[Vai trò + kinh nghiệm + context ngành]
</role>

<context>
[Bối cảnh tình huống — ai đang hỏi, từ đâu, mục đích gì]
</context>

<instructions>
[Hướng dẫn chi tiết]
1. [Step 1]
2. [Step 2]
NGUYÊN TẮC: Chỉ dùng thông tin từ <data>, không suy đoán
</instructions>

<constraints>
- [Điều không được làm 1]
- [Điều không được làm 2]
- Output phải có [yêu cầu bắt buộc]
</constraints>

<data>
[Dữ liệu thực tế: hợp đồng, báo cáo, transcript, CSV...]
</data>

<output_format>
[Template output — Claude điền vào]
## [Tiêu đề]
### [Section 1]
[...]
</output_format>
```

---

## TEMPLATE 3: Anti-Hallucination (cho Finance / Legal / Compliance)

```
<role>
[Financial Controller / Legal Analyst / Compliance Officer]
Ưu tiên accuracy tuyệt đối, không suy đoán.
</role>

<instructions>
Phân tích tài liệu trong <source_data> và:
1. [Task cụ thể]
2. [Task cụ thể]

NGUYÊN TẮC BẮT BUỘC:
- CHỈ trích dẫn từ <source_data> — không thêm thông tin bên ngoài
- Mỗi nhận định phải kèm [Nguồn: trang X / điều Y / mục Z]
- Nếu không có trong tài liệu → viết rõ "Tài liệu không đề cập"
- Đánh dấu [⚠️ CẦN KIỂM CHỨNG] với bất kỳ điểm không chắc
</instructions>

<source_data>
[Dán tài liệu gốc]
</source_data>

<output_format>
[Format output + yêu cầu citation]
</output_format>
```

---

## TEMPLATE 4: Few-Shot (dạy bằng ví dụ)

```
<role>[Vai trò]</role>

<instructions>
[Mô tả task]
Xem <examples> để hiểu format output mong muốn.
</instructions>

<examples>
Ví dụ 1:
Input: [input mẫu 1]
Output: [output mẫu 1]

Ví dụ 2:
Input: [input mẫu 2]
Output: [output mẫu 2]
</examples>

<input>
[Input thực tế cần xử lý]
</input>
```

---

## TEMPLATE 5: Batch Processing (xử lý nhiều items)

```
<role>[Vai trò]</role>

<instructions>
Xử lý từng item trong <items> theo cùng một format.
Với mỗi item:
1. [Step 1]
2. [Step 2]
Không bỏ qua item nào — nếu thiếu data ghi "[Cần thêm thông tin]"
</instructions>

<items>
Item 1: [nội dung]
Item 2: [nội dung]
Item 3: [nội dung]
</items>

<output_format>
## Item 1: [tên]
[output]

## Item 2: [tên]
[output]
</output_format>
```

---

## TEMPLATE 6: Pipeline 2 bước (Analyze → Recommend)

```
<role>[Expert trong lĩnh vực phân tích]</role>

<instructions>
BƯỚC 1 — PHÂN TÍCH:
- [Phân tích dimension 1]
- [Phân tích dimension 2]
- [Phân tích dimension 3]

BƯỚC 2 — ĐỀ XUẤT:
- Dựa trên phân tích bước 1, đề xuất [N] hành động cụ thể
- Mỗi đề xuất: [action] + [lý do] + [timeline ước tính]
- Ưu tiên theo impact: P0 (làm ngay) → P1 (trong tuần) → P2 (trong tháng)
</instructions>

<data>[Dữ liệu phân tích]</data>

<output_format>
## PHÂN TÍCH
[Kết quả bước 1]

## ĐỀ XUẤT
### P0 — Làm ngay
- [Action]: [lý do]

### P1 — Trong tuần
- [Action]: [lý do]

### P2 — Trong tháng
- [Action]: [lý do]
</output_format>
```

---

## TEMPLATE 7: Verification Prompt (Review output AI vừa tạo)

```
Hãy review lại câu trả lời vừa rồi:
1. Có điểm nào không chắc 100%? → Đánh dấu [⚠️ CẦN KIỂM CHỨNG]
2. Có điểm nào không có trong dữ liệu gốc? → Loại bỏ hoặc ghi rõ nguồn
3. Có câu nào có thể hiểu nhầm? → Sửa lại cho rõ hơn
4. Format có đúng yêu cầu không? → Adjust nếu cần

Sau review, xuất bản lại output đã được cải thiện.
```

---

## Tips dùng XML tags hiệu quả

| Tình huống | Nên làm |
|-----------|---------|
| Prompt < 100 từ, brainstorm | Không cần XML — viết thẳng |
| Prompt có data cụ thể | Dùng `<data>` để tách instruction và data |
| Prompt phức tạp, nhiều bước | Dùng template 2 (đầy đủ) |
| Output phải nhất quán cho team | Specify rõ trong `<output_format>` |
| Task financial/legal/compliance | Dùng template 3 (anti-hallucination) |
| Học từ ví dụ cụ thể | Dùng template 4 (few-shot) |

**Thứ tự tag được khuyến nghị:**
`<role>` → `<context>` → `<instructions>` → `<constraints>` → `<examples>` → `<data>` → `<output_format>` → `<post_action>`
