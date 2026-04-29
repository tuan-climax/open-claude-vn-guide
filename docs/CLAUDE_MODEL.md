# Hướng dẫn phân loại Task theo Claude Models (Haiku / Sonnet / Opus)

> **Cập nhật:** 29/04/2026 | Áp dụng cho Claude Haiku 4.5, Sonnet 4.6, Opus 4.7
> **Đối tượng:** Dân văn phòng, developer, knowledge worker

---

## 1. Tổng quan 3 models

| Tiêu chí | Haiku 4.5 | Sonnet 4.6 | Opus 4.7 |
|---|---|---|---|
| **Giá Input** ($/1M tokens) | $1 | $3 | $5 |
| **Giá Output** ($/1M tokens) | $5 | $15 | $25 |
| **Context window** | 200K tokens | 1M tokens | 1M tokens |
| **Tốc độ output** | 80–120 tok/s | 40–60 tok/s | 20–30 tok/s |
| **SWE-bench Verified** | 73.3% | 79.6% | ~80.8%+ |
| **Vai trò** | Volume workhorse | Default cho 80% task | Frontier reasoning |
| **So với Sonnet** | Rẻ hơn 3x, nhanh 2x | Baseline | Đắt hơn 1.67x, chậm 2x |

### Nguyên tắc lõi (rule of thumb)

- **Mặc định: Sonnet 4.6** — sweet spot cho hầu hết công việc (coding, viết tài liệu, phân tích, tool calling).
- **Hạ xuống Haiku 4.5** khi: task đơn giản, lặp lại, chạy số lượng lớn, hoặc cần tốc độ phản hồi nhanh.
- **Lên Opus 4.7** khi: task có rủi ro cao nếu sai (chiến lược, kiến trúc hệ thống), reasoning đa bước phức tạp, hoặc kết quả ảnh hưởng trực tiếp đến quyết định lớn.

### Test 3 câu hỏi trước khi chọn model

1. **Sai có hậu quả nghiêm trọng không?** → Có → cân nhắc Opus. Không → Sonnet hoặc Haiku.
2. **Có cần reasoning đa bước (>3 bước logic phụ thuộc nhau) không?** → Có → Sonnet/Opus. Không → Haiku ổn.
3. **Volume bao nhiêu?** → >1000 lần/ngày → Haiku để tiết kiệm. Thỉnh thoảng → khỏi quan tâm chi phí.

---

## 2. CLAUDE HAIKU 4.5 — Volume Workhorse

**Đặc điểm:** Nhanh, rẻ, đủ thông minh cho task có pattern rõ ràng. Phù hợp tích hợp vào pipeline tự động chạy số lượng lớn.

**Khi nào dùng:**
- Task có cấu trúc input/output rõ ràng, lặp lại
- Cần throughput cao (xử lý hàng nghìn record)
- Latency quan trọng hơn độ tinh tế
- Classification, extraction, routing, simple Q&A

**Khi nào KHÔNG dùng:**
- Task đòi hỏi reasoning sâu hoặc judgement phức tạp
- Code có logic nghiệp vụ phức tạp, nhiều file phụ thuộc
- Quyết định chiến lược, viết nội dung yêu cầu sự tinh tế cao

### 20 Task ví dụ phù hợp với Haiku 4.5

#### Văn phòng & Hành chính

1. **Phân loại email** vào folder: công việc / khách hàng / spam / nội bộ.
2. **Tóm tắt ngắn (1–2 câu)** từng email/tin nhắn dài để xem nhanh.
3. **Trích xuất thông tin từ form** — tên, email, số điện thoại, địa chỉ từ văn bản tự do.
4. **Standardize tên** — gộp các biến thể về dạng chuẩn (ví dụ: "Cty TNHH ABC", "ABC Co.,Ltd", "ABC Limited").
5. **Soát chính tả & lỗi đánh máy** trên văn bản ngắn (email, tin nhắn nội bộ).
6. **Convert đơn vị** trong file dữ liệu (USD↔VND, kg↔tấn, °C↔°F).
7. **Auto-tag ticket support** vào danh mục: lỗi kỹ thuật / hỏi giá / khiếu nại / yêu cầu feature.
8. **Sentiment analysis cơ bản** trên feedback khách hàng (positive/neutral/negative).
9. **Sinh email template trả lời** với placeholder điền sẵn (xác nhận đặt hàng, cảm ơn, follow-up).
10. **Format dữ liệu** — chuyển ngày tháng, số điện thoại, tiền tệ về format chuẩn.

#### Code & Dữ liệu

11. **Sinh boilerplate code** — class skeleton, CRUD endpoint, basic component.
12. **Format & lint suggestion** — đề xuất sửa code style theo chuẩn (PEP8, prettier).
13. **Viết docstring/comment** cho hàm đã có sẵn.
14. **Convert format file** — JSON ↔ CSV ↔ XML với schema cố định.
15. **Tạo regex pattern** cho task parsing đơn giản (extract số điện thoại, email, mã số).
16. **Validate format dữ liệu** — kiểm tra row CSV có đúng schema không.
17. **Detect anomaly đơn giản** — flag row có giá trị lệch quá X std deviation so với mean.
18. **Translate SQL đơn giản → Python pandas** (SELECT, WHERE, GROUP BY cơ bản).
19. **Đặt tên biến/hàm** theo convention từ mô tả ngắn.
20. **Sinh test data giả** (fake users, fake transactions) theo schema có sẵn.

> **Tip:** Trong pipeline tự động hóa, dùng Haiku để filter/classify ở bước đầu, chỉ những case "khó" mới đẩy lên Sonnet xử lý. Cách này có thể tiết kiệm 60–70% chi phí so với chạy Sonnet toàn bộ.

---

## 3. CLAUDE SONNET 4.6 — Default Daily Driver

**Đặc điểm:** Đạt 99% chất lượng Opus với 40% chi phí và tốc độ gấp đôi. Là "default" cho mọi task không quá đơn giản (Haiku) cũng không quá phức tạp (Opus).

**Khi nào dùng:**
- Coding hằng ngày: viết feature, debug, refactor vừa phải
- Phân tích cần reasoning vài bước
- Viết tài liệu nghiệp vụ, báo cáo, đề xuất
- Tool calling, agentic workflow vừa phải
- Khi không chắc chọn model nào → chọn Sonnet

**Khi nào KHÔNG dùng:**
- Task đơn giản, lặp lại số lượng lớn → Haiku
- Quyết định chiến lược cấp công ty, kiến trúc hệ thống lớn → Opus
- Debug bug logic phức tạp đã thử nhiều lần không xong → Opus

### 20 Task ví dụ phù hợp với Sonnet 4.6

#### Văn phòng & Knowledge Work

1. **Soạn email quan trọng** — gửi cho khách hàng VIP, sếp, đối tác (cần tinh tế tone).
2. **Viết báo cáo công việc tuần/tháng** — tổng hợp data từ nhiều nguồn, có insight và đề xuất.
3. **Tóm tắt cuộc họp/transcript dài** — extract action items, decision, next step.
4. **Soạn proposal/đề xuất** cho dự án nội bộ — gồm vấn đề, giải pháp, timeline, resource.
5. **Phân tích dữ liệu Excel** vừa phải — pivot, trend analysis, viết insight bằng văn bản.
6. **Soạn slide deck content** — viết text cho từng slide thuyết trình (không lo phần thiết kế).
7. **Viết JD tuyển dụng** — phân tích yêu cầu kỹ năng, mô tả văn hóa, benefit package.
8. **Soạn SOP (Standard Operating Procedure)** cho quy trình nghiệp vụ.
9. **Phân tích cạnh tranh cơ bản** — so sánh 3–5 đối thủ về feature, pricing, positioning.
10. **Viết User Story + Acceptance Criteria** cho feature mới.

#### Code & Development

11. **Viết feature mới** — bao gồm logic, error handling, validation, basic test.
12. **Refactor module** — tách hàm, đổi tên, cải thiện readability.
13. **Debug bug thông thường** — đọc log, trace lỗi, đề xuất fix.
14. **Viết SQL query phức tạp** — multi-join, window function, CTE.
15. **Build API endpoint** — kèm validation, auth, rate limit cơ bản (FastAPI/Flask/Express).
16. **Tích hợp third-party API** — Stripe, Google Maps, OpenAI, webhook handler.
17. **Viết unit test** cho code đã có.
18. **Convert Excel logic phức tạp sang code** — file có nhiều VLOOKUP, INDEX/MATCH lồng nhau.
19. **Viết script automation** — kết hợp đọc email, xử lý file, push data lên DB.
20. **Build component UI** với React/Vue + framework CSS (form, dashboard, table với filter).

> **Tip:** Sonnet là model nên dùng mặc định trong IDE (VS Code, Cursor, Claude Code) cho công việc coding hàng ngày. Chỉ chuyển sang Opus khi gặp bug logic phức tạp Sonnet sửa hoài không xong, hoặc khi thiết kế kiến trúc hệ thống quan trọng.

---

## 4. CLAUDE OPUS 4.7 — Frontier Reasoning

**Đặc điểm:** Model thông minh nhất hiện tại của Anthropic, vượt trội ở task yêu cầu reasoning đa bước, planning dài hạn, và judgement tinh tế. Đắt và chậm — chỉ dùng khi thực sự cần.

**Lưu ý quan trọng:** Opus 4.7 dùng tokenizer mới có thể tốn tới 35% token nhiều hơn cho cùng một đoạn text. Chi phí thực tế có thể cao hơn rate card.

**Khi nào dùng:**
- Quyết định chiến lược cấp công ty (rủi ro cao nếu sai)
- Kiến trúc hệ thống phức tạp, ảnh hưởng dài hạn
- Reasoning đa bước (>5 bước logic phụ thuộc lẫn nhau)
- Agentic workflow tự chủ chạy nhiều giờ
- Nghiên cứu khoa học, modeling tài chính phức tạp
- Viết tài liệu pháp lý, hợp đồng (instruction following precision matters)

**Khi nào KHÔNG dùng:**
- Task có Sonnet làm tốt rồi (đừng overpay)
- Task volume cao chạy hằng ngày (đốt tiền)
- Coding thông thường (Sonnet đạt 99% Opus với giá 40%)

### 20 Task ví dụ phù hợp với Opus 4.7

#### Chiến lược & Quyết định lớn

1. **Xây dựng business plan/business model canvas** đầy đủ — phân tích revenue stream, cost structure, scenarios.
2. **Lập tài chính 3–5 năm (financial projection)** — bao gồm CAC, LTV, churn rate, multiple scenarios (bear/base/bull).
3. **Thiết kế pricing strategy** đa tier — phân tích giá đối thủ, willingness-to-pay, cannibalization risk.
4. **Phân tích go-to-market strategy** — chọn segment ưu tiên, kênh phân phối, timing, risk.
5. **Soạn pitch deck cho VC/investor** — không chỉ viết text mà reasoning về angle convince, why now, why us.
6. **Đánh giá quyết định build vs buy** — phân tích ROI giữa tự build vs license, kèm risk matrix.
7. **Phân tích M&A / partnership** — đánh giá strategic fit, valuation, integration risk.
8. **Soạn term sheet / cap table modeling** — equity dilution, vesting, anti-dilution clauses.

#### Kiến trúc & Hệ thống phức tạp

9. **Thiết kế kiến trúc end-to-end** cho hệ thống lớn — từ ingestion → processing → storage → serving, kèm trade-off từng lựa chọn.
10. **Refactor codebase lớn** — khi cần thay đổi kiến trúc cốt lõi (monolith → microservice), cần reasoning về dependency và migration strategy.
11. **Debug bug logic phức tạp** mà Sonnet đã thử mà không sửa được — race condition, memory leak, edge case ẩn sâu.
12. **Thiết kế hệ thống multi-tenant SaaS** — isolation, billing, quota, security model.
13. **Đánh giá lựa chọn tech stack** cho vấn đề mở — kèm benchmark và TCO analysis.
14. **Tối ưu pipeline ML/data phức tạp** — phân tích bottleneck, đề xuất cải tiến có roadmap.

#### Phân tích chuyên sâu & Pháp lý

15. **Nghiên cứu phương pháp luận mới** — thiết kế methodology, weight, validation rule.
16. **Đọc & phân tích bài báo nghiên cứu** — đánh giá có áp dụng được không, đề xuất experiment plan.
17. **Modeling kịch bản phức tạp** — Monte Carlo simulation, sensitivity analysis với nhiều biến.
18. **Phân tích pháp lý** — rủi ro hợp đồng, GDPR/PDPA compliance, IP, data residency.
19. **Soạn thảo hợp đồng quan trọng** — partnership agreement, employment contract cấp C-level, NDA.
20. **Thiết kế cơ cấu tổ chức** khi scale lớn — role design, reporting structure, decision rights, RACI matrix.

> **Tip:** Với các quyết định ảnh hưởng dài hạn (chiến lược, kiến trúc, pháp lý), đầu tư thêm vài đô cho Opus reasoning kỹ là đáng giá hơn rất nhiều so với việc model rẻ hơn đưa ra answer "ổn-ổn" rồi đi sai đường nhiều tháng.

---

## 5. Chiến lược Routing tối ưu

### Phân bổ ngân sách gợi ý ($500/tháng)

| Model | % Budget | Use case |
|---|---|---|
| Haiku 4.5 | 50% (~$250) | Pipeline tự động, classification, simple automation |
| Sonnet 4.6 | 40% (~$200) | Coding hàng ngày, viết tài liệu, phân tích thông thường |
| Opus 4.7 | 10% (~$50) | Quyết định chiến lược lớn, kiến trúc hệ thống, debug khó |

### Pattern thực tế

**Cho dân văn phòng:**
- Email/tin nhắn ngắn → Haiku
- Báo cáo, proposal, slide → Sonnet
- Quyết định chiến lược, soạn hợp đồng → Opus

**Cho developer:**
- Format code, sinh boilerplate, viết docstring → Haiku
- Coding feature hàng ngày, debug thông thường, refactor module → Sonnet
- Thiết kế kiến trúc, debug bug khó nhằn, refactor codebase lớn → Opus

### 2 đòn bẩy giảm chi phí

1. **Prompt caching:** Nếu dùng cùng một system prompt lặp lại (ví dụ: cùng instruction phân loại) → bật `cache_control` để giảm tới 90% chi phí input. Cached input của Opus chỉ ~$0.50/M, rẻ hơn cả Haiku standard.
2. **Batch processing:** Task không cần real-time → dùng Batch API giảm 50% chi phí.

---

## 6. Các sai lầm thường gặp cần tránh

1. **Default everything về Opus** — đốt tiền vô ích. Sonnet đủ tốt cho 80% task.
2. **Cố ép Haiku làm task phức tạp** — Haiku trả lời nhanh nhưng sai logic, mất nhiều thời gian fix manual hơn là dùng Sonnet ngay từ đầu.
3. **Không bật prompt caching** cho task lặp lại — bỏ lỡ giảm 90% chi phí input.
4. **Chuyển model giữa session** mà không reset context — gây inconsistent output.
5. **Dùng Opus cho code thông thường** — Sonnet 4.6 đạt 79.6% SWE-bench vs Opus 80.8%, gap 1.2% không xứng đáng với 40% giá đắt hơn cho coding.

---

**Nguồn tham khảo:**
- Anthropic Pricing: https://platform.claude.com/docs/en/about-claude/pricing
- Models Overview: https://platform.claude.com/docs/en/about-claude/models/overview
- Tài liệu này tổng hợp dựa trên data từ tháng 4/2026, sẽ cần update khi Anthropic ra model mới.
