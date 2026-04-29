# Claude AI Kit (Generic)

Bộ Claude Code assets chuẩn hoá — cài đặt một lần, cả team dùng ngay. Dùng được cho mọi tổ chức, mọi ngành.

> Tài liệu hướng dẫn đầy đủ: xem **Claude_AI_Kit_Generic.docx** đi kèm kit này.

## Cài đặt nhanh

```bash
# 1. Cài Claude Code (yêu cầu Node.js 18+)
npm install -g @anthropic-ai/claude-code

# 2. Copy thư mục này về project của bạn (hoặc dùng làm global kit)
cp -r generic-claude-kit/.claude ~/.claude   # dùng global
# hoặc copy vào root của project cụ thể

# 3. Chỉnh CLAUDE.md theo thông tin công ty bạn
# (xem templates/CLAUDE.md để có version có placeholders)

# 4. Mở Claude Code
claude
# Claude tự đọc CLAUDE.md, load rules và skills
```

## Cấu trúc

```
generic-claude-kit/
├── README.md                          ← file này
├── CLAUDE.md                          ← context công ty (tự động load mỗi session)
├── .claude/
│   ├── settings.json                  ← permissions + hooks + env vars
│   ├── rules/
│   │   ├── data-conventions.md        ← SQL naming, data engineering standards
│   │   ├── content-style.md           ← brand voice, tone guide template
│   │   └── coding-conventions.md      ← coding standards (điều chỉnh theo stack)
│   ├── skills/
│   │   ├── deal-briefing/             ← Sales: brief trước cuộc họp
│   │   ├── content-repurpose/         ← Marketing: 1 bài → 4 format
│   │   ├── research-synthesis/        ← BA/Product: tổng hợp transcript
│   │   ├── data-quality-check/        ← Data: kiểm tra data quality
│   │   ├── reconciliation/            ← Finance: đối soát & variance
│   │   ├── onboarding-kit-gen/        ← HR: kit nhân viên mới
│   │   ├── code-review/               ← Dev: review PR theo checklist
│   │   └── prompt-builder/            ← All: xây prompt chuẩn từ đầu
│   └── agents/
│       ├── data-scientist.md          ← SQL/data expert persona
│       ├── content-reviewer.md        ← Brand voice guardian
│       └── code-reviewer.md           ← Engineering standards reviewer
├── templates/                         ← Templates có placeholder để tuỳ chỉnh
│   ├── CLAUDE.md                      ← CLAUDE.md tổ chức (có [Tên công ty])
│   ├── project-CLAUDE.md              ← CLAUDE.md cho project Dev
│   ├── settings.json                  ← settings mẫu
│   └── agents/                        ← Agent.md cho từng phòng ban
│       ├── HR-agent.md
│       ├── Finance-agent.md
│       ├── Marketing-agent.md
│       ├── Sales-agent.md
│       ├── BA-agent.md
│       ├── Data-agent.md
│       └── Dev-agent.md
└── docs/
    ├── CLAUDE_CODE_COMMANDS.md        ← Cheatsheet 30+ slash commands
    ├── CLAUDE_HOWTO_SUMMARY.md        ← MCP, Hooks, Skills guide tóm tắt
    ├── CLAUDE_MODEL.md                ← Model, Tasks for model
    └── prompt-library/                ← Templates rời theo phòng ban
        ├── xml-templates.md           ← XML prompt templates đầy đủ
        ├── HR_templates.md
        ├── Sales_templates.md
        ├── Marketing_templates.md
        ├── Finance_templates.md
        ├── Data_templates.md
        ├── BA_templates.md
        └── Dev_templates.md
```

## Skills có sẵn

| Skill | Phòng ban | Trigger phrases |
|-------|-----------|-----------------|
| `deal-briefing` | Sales | "deal brief", "brief khách", "/deal-brief" |
| `content-repurpose` | Marketing | "repurpose", "1 bài 4 format", "/repurpose" |
| `research-synthesis` | BA/Product | "tổng hợp transcript", "themes", "/synthesize" |
| `data-quality-check` | Data | "data quality", "kiểm tra data", "/dq-check" |
| `reconciliation` | Finance | "đối soát", "reconciliation", "/recon" |
| `onboarding-kit-gen` | HR | "onboarding", "nhân viên mới", "/onboard" |
| `code-review` | Dev | "code review", "review PR", "/review" |
| `prompt-builder` | All | "xây prompt", "tạo prompt", "/build-prompt" |

## Agents có sẵn

```bash
# Gọi agent trong Claude Code:
"Use the data-scientist agent to..."
"Act as content-reviewer and..."
"Switch to code-reviewer mode"
```

## Hooks đã cấu hình

- **PreToolUse**: Block write vào `.env`, `credentials`, `secret` files
- **PostToolUse**: Log mọi file thay đổi vào `.claude/change.log`
- **Stop**: Nhắc `/compact` khi kết thúc session

## Tuỳ chỉnh theo công ty bạn

1. Chỉnh `CLAUDE.md` — thêm tên công ty, ngành, brand voice, quy tắc
2. Chỉnh `.claude/rules/` — cập nhật stack, coding conventions, content style
3. Chỉnh skill files — thay `[Tên công ty]` và `[sản phẩm]` trong các skill
4. Xem `templates/` để có các mẫu chưa điền sẵn

## Cần hỗ trợ

- Issues / báo lỗi: GitHub Issues
- Thảo luận: GitHub Discussions
- Đóng góp template / Skill mới: Pull Request

## Disclaimer (Miễn trừ trách nhiệm)
Dự án này không thuộc sở hữu hoặc được ủy quyền bởi Anthropic. Đây là tài liệu hướng dẫn từ cộng đồng.
