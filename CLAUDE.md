# [Tên công ty] — Claude AI Context

<!-- Thay [Tên công ty] và các placeholder bên dưới theo thông tin công ty bạn -->
<!-- Giữ file này < 2.000 token — thông tin chi tiết hơn → load-on-demand qua @docs/ -->

## Về công ty
[Tên công ty] cung cấp [sản phẩm/dịch vụ] cho [phân khúc khách hàng].
- Quy mô: ~[N] nhân viên | Địa điểm: [Thành phố]
- Ngành: [Ngành/lĩnh vực]
- Khách hàng: [Loại khách hàng chính]

## Sản phẩm / Dịch vụ chính
- **[Tên sản phẩm 1]**: [Mô tả ngắn]
- **[Tên sản phẩm 2]**: [Mô tả ngắn]
- **[Tên dịch vụ]**: [Mô tả ngắn]

## Cơ cấu tổ chức
- **[Phòng ban 1]** — [chức năng chính]
- **[Phòng ban 2]** — [chức năng chính]
- **[Phòng ban 3]** — [chức năng chính]
<!-- Điền theo cơ cấu thực tế: Data, Sales, Marketing, BA/Product, Dev, HR, Finance... -->

## Brand Voice
- [Tính cách 1, vd: chuyên nghiệp, data-driven, chính xác]
- Tiếng Việt là ngôn ngữ chính; giữ tiếng Anh cho thuật ngữ chuyên ngành
- [Điều nên tránh trong giao tiếp, vd: không dùng hype, không cường điệu]
- Tone với khách hàng: [formal/informal/balanced] — [đặc điểm thêm]

## Quy tắc bắt buộc (KHÔNG được vi phạm)
1. KHÔNG tiết lộ thông tin nhạy cảm của khách hàng (dữ liệu, hợp đồng, tài chính)
2. Trích dẫn nguồn cụ thể khi đề cập số liệu
3. Khi không chắc chắn → nói rõ mức độ tin cậy và hướng dẫn liên hệ đúng người
4. Output liên quan tài chính/pháp lý → PHẢI có human review trước khi dùng thật
5. Không write/commit file nhạy cảm: .env, credentials, private keys

## Rules (load khi cần — dùng @filename)
- `@.claude/rules/data-conventions.md` — SQL naming, data engineering conventions
- `@.claude/rules/content-style.md` — brand guide, content templates
- `@.claude/rules/coding-conventions.md` — coding standards

## Skills thư viện
Gọi bằng trigger phrase hoặc /skill-name. Xem README.md để biết danh sách đầy đủ.
