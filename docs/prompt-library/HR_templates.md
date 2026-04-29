# HR Prompt Templates
<!-- v1.0 | 2026-04-29 | generic -->

## CÁCH DÙNG
Copy prompt → paste vào Claude → điền vào `[...]` → gửi.

---

## HR-01: Viết Job Description

```
<role>HR Business Partner, chuyên tuyển dụng [tech / fintech / retail / ngành của bạn]</role>

<instructions>
Viết Job Description cho vị trí [TÊN VỊ TRÍ]:
1. Tên vị trí và phòng ban
2. Mô tả công việc chính (5-7 bullet, bắt đầu bằng động từ)
3. Yêu cầu bắt buộc (4-5 điều kiện Must-have)
4. Yêu cầu ưu tiên (2-3 điều kiện Nice-to-have)
5. Quyền lợi hấp dẫn (5-6 bullet, cụ thể — không chung chung)
6. Thông tin ứng tuyển
</instructions>

<context>
Công ty: [Tên công ty] — [ngành], [quy mô] người, [thành phố]
Văn hóa: [mô tả văn hóa công ty]
Cấp độ: [Junior/Mid/Senior]
Lương: [X-Y triệu VNĐ]
Yêu cầu kinh nghiệm: [N năm]
Điểm đặc biệt của vị trí: [điền vào]
</context>

<output_format>
Tone: chuyên nghiệp nhưng thân thiện, thu hút ứng viên target
Độ dài: 400-500 từ
Ngôn ngữ: Tiếng Việt, giữ tiếng Anh cho thuật ngữ kỹ thuật
</output_format>
```

---

## HR-02: Performance Review Draft

```
<role>HR Business Partner hỗ trợ manager viết performance review constructive và fair</role>

<instructions>
Viết performance review cho nhân viên dưới đây:
1. Tổng điểm và nhận xét tổng quan (2-3 câu)
2. Đánh giá chi tiết từng KPI (theo bảng bên dưới)
3. Điểm mạnh nổi bật (2-3 điểm, có ví dụ cụ thể)
4. Cần cải thiện (1-2 điểm, framed as opportunity, không blame)
5. SMART Goals cho quý tiếp theo (3 goals)
6. Đề xuất phát triển (training, project, stretch assignment)
</instructions>

<employee_data>
Tên: [Tên nhân viên]
Vị trí: [Vị trí]
Kỳ đánh giá: [Q? / Năm?]
KPI Framework:
- Chất lượng công việc (30%): điểm [X/5]
- Tiến độ hoàn thành (25%): điểm [X/5]
- Sáng kiến & đổi mới (20%): điểm [X/5]
- Teamwork (15%): điểm [X/5]
- Phát triển bản thân (10%): điểm [X/5]
Ghi chú bổ sung: [thành tích nổi bật, incident cần mention]
</employee_data>

<constraints>
- Balanced và constructive — không chỉ tích cực, không chỉ tiêu cực
- Có dẫn chứng cụ thể (không nhận xét chung chung)
- Goals phải SMART (Specific, Measurable, Achievable, Relevant, Time-bound)
- KHÔNG mention thông tin lương trong văn bản này
</constraints>
```

---

## HR-03: Policy Q&A

```
<role>HR Assistant — trả lời câu hỏi về chính sách nhân sự</role>

<instructions>
Trả lời câu hỏi dưới đây dựa trên nội quy công ty được cung cấp:
- Câu trả lời ngắn gọn, rõ ràng (3-5 câu)
- Trích dẫn điều khoản cụ thể [Chương X, Mục Y]
- Nếu nội quy chưa quy định → nói rõ và khuyến nghị hỏi HR trực tiếp
- KHÔNG suy đoán chính sách
</instructions>

<company_policy>
[Paste đoạn nội quy liên quan]
</company_policy>

<question>
[Câu hỏi của nhân viên]
</question>

<output_format>
Trả lời: [câu trả lời]
Căn cứ: [Chương X, Mục Y của nội quy]
Lưu ý: [điều gì cần clarify thêm nếu có]
</output_format>
```

---

## HR-04: Interview Question Set

```
<role>Senior HR Interviewer, chuyên behavioral interview</role>

<instructions>
Tạo bộ câu hỏi phỏng vấn cho vị trí [TÊN VỊ TRÍ]:
1. Technical questions (3-4 câu): kiểm tra hard skills
2. Behavioral questions (3-4 câu STAR format): kiểm tra culture fit
3. Situational questions (2-3 câu): phản ứng trong tình huống cụ thể
4. Culture fit questions (2 câu): giá trị, working style
5. Candidate's questions to ask us (gợi ý để candidate hỏi ngược lại)

Với mỗi câu: ghi thêm "Đánh giá gì?" và "Red flags cần chú ý"
</instructions>

<context>
Vị trí: [TÊN VỊ TRÍ]
Cấp độ: [Junior/Mid/Senior]
Yêu cầu đặc biệt: [kỹ năng hoặc trait quan trọng nhất]
Giá trị công ty: [điền values của công ty bạn]
</context>
```

---

## HR-05: Onboarding Kit Nhanh

```
<role>HR Business Partner tạo onboarding kit cho nhân viên mới</role>

<instructions>
Tạo onboarding kit cho nhân viên mới gồm:
1. Welcome message (3 câu, cá nhân hoá theo tên và vị trí)
2. Checklist ngày đầu (7 items)
3. Checklist tuần đầu (7 items)
4. 5 người cần gặp + lý do
5. 3 câu hỏi phúc lợi thường gặp + trả lời ngắn
</instructions>

<new_hire>
Tên: [Tên]
Vị trí: [Vị trí]
Phòng ban: [Phòng ban]
Ngày bắt đầu: [Ngày]
</new_hire>

<company_policy>
[Paste đoạn chính sách phúc lợi nếu có]
</company_policy>
```
