# Sales Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.

---

## SALES-01: Deal Briefing trước cuộc họp

```
<role>Sales Director B2B, chuyên enterprise clients</role>

<instructions>
Chuẩn bị brief trước cuộc họp với khách hàng dưới đây. Gồm:
1. Snapshot công ty (3 dòng: ngành, quy mô, vị thế)
2. Pain points dự đoán (3-4 điểm, có lý do cụ thể)
3. Sản phẩm/dịch vụ phù hợp nhất (2-3 items với lý do)
4. 5 câu hỏi khám phá nhu cầu (open-ended)
5. Watch out: rủi ro hoặc điểm nhạy cảm
</instructions>

<client_info>
Tên công ty: [Tên]
Ngành: [Ngành]
Quy mô: [N nhân viên / doanh thu]
Người gặp: [Tên và chức vụ]
Đang dùng: [Tool/giải pháp hiện tại nếu biết]
Bối cảnh: [Lý do họ muốn gặp]
</client_info>

<our_products>
[Mô tả ngắn sản phẩm/dịch vụ của công ty bạn — 2-3 dòng/sản phẩm]
</our_products>
```

---

## SALES-02: Proposal / Đề xuất giải pháp

```
<role>Senior Sales Consultant, chuyên viết proposals cho B2B</role>

<instructions>
Viết proposal cho khách hàng dưới đây:
1. Executive Summary (1 trang, tập trung vào ROI)
2. Hiểu vấn đề (Pain points đã xác nhận)
3. Giải pháp đề xuất (liên kết từng feature → pain point)
4. Tại sao chọn chúng tôi (3 lý do differentiation)
5. Investment & Timeline
6. Next steps
</instructions>

<context>
Khách hàng: [Thông tin từ deal brief hoặc discovery call]
Sản phẩm đề xuất: [Tên sản phẩm + tier]
Giá: [Range hoặc custom — chỉ mention nếu đã approved]
Timeline triển khai: [N tuần/tháng]
</context>

<constraints>
- Tập trung vào giá trị, không liệt kê tính năng
- Mọi claim phải có số liệu hoặc case study hỗ trợ
- Không đề cập giá khi chưa được authorized
- Tone: professional + consultative, không "sales-y"
</constraints>
```

---

## SALES-03: Email Follow-up sau Demo/Meeting

```
<role>Sales Executive, viết email follow-up ngắn gọn và có giá trị</role>

<instructions>
Viết email follow-up sau cuộc họp với:
1. Cảm ơn + 1 điểm highlight từ cuộc họp
2. Tóm tắt 2-3 điểm đã thảo luận và thống nhất
3. Next steps rõ ràng (ai làm gì, deadline)
4. 1 resource hữu ích liên quan đến pain point họ đề cập
</instructions>

<meeting_notes>
Ngày họp: [Ngày]
Người tham dự: [Tên khách + tên mình]
Những gì đã thảo luận: [Ghi chú ngắn]
Pain points xác nhận: [List]
Next steps đã đồng ý: [List]
</meeting_notes>

<output_format>
Subject: [Re: meeting title] — Follow-up + Next Steps

Kính gửi anh/chị [Tên],

[Cảm ơn + điểm highlight]

[Tóm tắt 2-3 điểm]

**Next steps:**
- [Action 1] — [người] — [deadline]
- [Action 2] — [người] — [deadline]

[Resource hữu ích nếu có]

Trân trọng,
[Tên]
</output_format>
```

---

## SALES-04: Objection Handling

```
<role>Senior Sales Advisor, chuyên xử lý objections trong B2B sales</role>

<instructions>
Với mỗi objection dưới đây, đề xuất:
1. Acknowledge: xác nhận concern của khách (không dismiss)
2. Reframe: đặt lại vấn đề từ góc độ khác
3. Evidence: dẫn chứng/case study hỗ trợ
4. Question: câu hỏi để tiếp tục conversation
</instructions>

<objections>
1. [Objection 1, vd: "Giá của các bạn cao hơn đối thủ"]
2. [Objection 2, vd: "Chúng tôi đã có giải pháp rồi"]
3. [Objection 3, vd: "Cần thời gian suy nghĩ thêm"]
</objections>

<our_strengths>
[3-5 điểm mạnh differentiation của sản phẩm/công ty bạn]
</our_strengths>
```

---

## SALES-05: Win/Loss Analysis

```
<role>Sales Analyst, phân tích deal để rút ra lessons learned</role>

<instructions>
Phân tích deal dưới đây:
1. Các yếu tố dẫn đến win/loss
2. Điểm nào trong sales process làm tốt
3. Điểm nào cần cải thiện
4. 3 lessons learned cho deals tương tự sau này
</instructions>

<deal_info>
Deal: [Tên khách / deal]
Kết quả: [Win / Loss]
Giá trị: [ARR/contract value]
Timeline: [Từ lead đến close: N tuần]
Lý do win/loss theo khách: [Nếu biết]
Ghi chú sales process: [Những gì đã xảy ra]
</deal_info>
```
