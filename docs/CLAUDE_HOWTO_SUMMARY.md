# Claude Code — HOWTO Tóm Tắt
> Claude Code v2.1+ | Tháng 4/2026  
> Nguồn: https://github.com/luongnv89/claude-howto

---

## 01 — Slash Commands & Skills

**Skills** (thay thế commands cũ):
- Lưu ở `.claude/skills/<tên>/SKILL.md`
- Tự động kích hoạt khi Claude đối chiếu description
- Gọi thủ công: `/skill-name` hoặc trigger phrase
- Frontmatter quan trọng: `name`, `description`, `triggers`

```yaml
---
name: my-skill
description: Khi nào skill này được gọi — mô tả cụ thể
triggers: ["trigger phrase", "/command"]
---
```

**Built-in skills sẵn:** `/batch`, `/simplify`, `/debug`, `/loop`, `/claude-api`

---

## 02 — Memory (Bộ Nhớ Liên Tục)

**Hệ phân cấp** (ưu tiên từ cao xuống):
1. `./CLAUDE.md` hoặc `./.claude/CLAUDE.md` — Project memory
2. `./.claude/rules/*.md` — Project rules
3. `~/.claude/CLAUDE.md` — User memory (tất cả projects)
4. `~/.claude/rules/*.md` — User rules
5. `./CLAUDE.local.md` — Local project (gitignore)

**Cập nhật nhanh:** Gõ `# quy tắc mới` trong chat → Claude hỏi lưu vào file nào

**Import tài liệu:** `@README.md` trong CLAUDE.md (hỗ trợ lồng 5 cấp)

**Auto Memory:** Claude tự ghi bài học vào `MEMORY.md` — load 200 dòng đầu mỗi session

---

## 03 — Skills: Cấu Trúc & Best Practices

**Progressive Disclosure (3 cấp):**
- Cấp 1: Metadata (~100 tokens) — luôn load khi khởi động
- Cấp 2: Nội dung SKILL.md (<5k tokens) — khi được gọi
- Cấp 3: Files hỗ trợ (scripts, templates) — khi cần

**Kiểm soát gọi:**
- `disable-model-invocation: true` — chỉ người dùng gọi thủ công
- `user-invocable: false` — chỉ Claude tự gọi
- `context: fork` — chạy trong subagent riêng (cô lập)

**Giới hạn:** Budget description là 2% context window — quá nhiều skills thì bị bỏ qua

---

## 04 — Subagents

**Built-in subagents:** `general-purpose`, `Plan`, `Explore` (Haiku, chỉ đọc), `Bash`, `Claude Code Guide`

**Cấu hình:** File `.md` trong `.claude/agents/` với YAML frontmatter:
```yaml
---
name: agent-name
description: Khi nào agent được gọi
model: claude-sonnet-4-6  # optional
maxTurns: 20              # optional
---
```

**Gọi agent:**
```
"Use the data-scientist agent to..."
"Use subagents to investigate X in parallel"
@"agent-name (agent)"
```

**Cô lập worktree:** `isolation: worktree` trong agent config — làm việc trên nhánh git riêng

---

## 05 — MCP (Model Context Protocol)

**Cài đặt:**
```bash
# HTTP (khuyến nghị)
claude mcp add --transport http github https://api.github.com/mcp

# Stdio (local)
claude mcp add --transport stdio postgres -- npx @company/db-server

# OAuth 2.0: tự động, lưu token vào system keychain
```

**MCP servers phổ biến:** GitHub, Jira, Slack, PostgreSQL, Google Docs, Stripe, Brave Search

**Phạm vi:** Local (chỉ bạn) | Project (`.mcp.json` — team) | User (tất cả projects)

**MCP → Slash Commands:** `/mcp__github__list_prs`, `/mcp__slack__send_message`

**Context Bloat:** Dùng code execution để gọi MCP tools thay vì truyền data qua model — giảm 98.7% token

---

## 06 — Hooks (Tự Động Hóa Sự Kiện)

**Các sự kiện chính:** `PreToolUse` (có thể chặn) | `PostToolUse` | `Stop` (có thể chặn) | `SessionStart` | `UserPromptSubmit`

**4 loại hook:** `command` (bash/python) | `prompt` (LLM đánh giá) | `http` (webhook) | `agent` (subagent check)

**Exit codes:** 0 = thành công | 2 = lỗi chặn (blocking) | khác = lỗi không chặn

**Ví dụ hay dùng:**
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{"type": "command", "command": "echo 'Changed: $CLAUDE_TOOL_INPUT_PATH' >> .claude/change.log"}]
    }],
    "PreToolUse": [{
      "matcher": "Write|Edit",
      "hooks": [{"type": "command", "command": "echo \"$CLAUDE_TOOL_INPUT_PATH\" | grep -qiE '(\\.env|secret|credentials)' && exit 1 || exit 0"}]
    }],
    "Stop": [{
      "hooks": [{"type": "command", "command": "echo 'Session ended — /compact if starting new task'"}]
    }]
  }
}
```

**Use cases phổ biến:**
- **PreToolUse**: Block write vào `.env`, `credentials` — prevent secrets leak
- **PostToolUse**: Log file changes, auto-format, scan hardcoded secrets
- **Stop**: Notify Slack/Teams khi task dài hoàn thành, nhắc `/compact`

---

## 07 — Plugins

**Cấu trúc plugin:**
```
.claude-plugin/
├── plugin.json        ← manifest
├── skills/            ← skills của plugin
├── agents/            ← agents của plugin
├── hooks/hooks.json   ← hooks của plugin
└── .mcp.json          ← MCP servers của plugin
```

**Cài đặt:**
```bash
/plugin install <tên>
/plugin install github:user/repo
claude --plugin-dir ./my-plugin
```

---

## 08 — Checkpoints (Undo)

- **Tự động:** Checkpoint sau mỗi prompt — không cần làm gì
- **Mở:** `Esc + Esc` hoặc `/rewind`
- **5 options:** Khôi phục code+hội thoại | Chỉ hội thoại | Chỉ code | Tóm tắt từ điểm này | Hủy
- **Giữ 30 ngày** rồi tự xóa
- **Lưu ý:** Bash commands (`rm`, `mv`) KHÔNG được track — vẫn cần git

---

## 09 — Advanced Features

| Feature | Command | Dùng khi |
|---------|---------|----------|
| Planning Mode | `/plan` hoặc `--permission-mode plan` | Task phức tạp — lập kế hoạch trước |
| Extended Thinking | `Alt+T` hoặc "ultrathink" | Reasoning sâu — đắt token |
| Auto Mode | `--enable-auto-mode` | Autonomous với safety check |
| Background Tasks | `Ctrl+B` | Task dài không block chat |
| Git Worktrees | `claude -w` | Thử nghiệm trên branch riêng |
| Voice | `/voice` | Push-to-talk input |
| Print Mode | `claude -p "query"` | CI/CD scripts, pipeline |

---

## 10 — CLI Reference Nhanh

```bash
claude                          # Session tương tác
claude -c                       # Tiếp tục session gần nhất
claude -r "tên"                 # Resume session đặt tên
claude -p "query"               # Non-interactive, 1 query
claude -p "q" --output-format json | jq  # JSON pipe
cat file.py | claude -p "review"         # Pipe file
claude --model opus             # Chọn model
claude --permission-mode plan   # Chỉ plan, không execute
claude --max-turns 10           # Giới hạn turns tự động
claude -w                       # Git worktree mode
```

---

## TIPS TIẾT KIỆM TOKEN

1. **Model Routing**: Haiku cho 80% tasks → Sonnet → Opus chỉ khi cần
2. **`/model opusplan`**: Auto Opus khi plan, Sonnet khi execute
3. **`MAX_THINKING_TOKENS: 10000`**: Giảm extended thinking cost ~2/3
4. **CLAUDE.md < 2K token**: Core only — chi tiết load-on-demand
5. **`/compact` định kỳ**: Trước task mới trong session dài
6. **Markitdown**: Convert PDF/DOCX → Markdown trước khi upload (giảm 90% token)
7. **Repomix**: Pack codebase → 1 file (giảm ~70% token)
8. **Output ngắn**: "No explanation, just the code" | "Diff only"

---

## LUỒNG LÀM VIỆC CHUẨN

```bash
# Bắt đầu task mới
claude
/plan
"[Mô tả task — Claude phân tích, KHÔNG code ngay]"
# → Review plan → Approve → Claude thực hiện

# Session dài
# Trước /compact: "Before compacting, preserve: (1) files modified (2) key decisions (3) next TODO"
/compact

# Sai hướng
Esc + Esc  # rewind về checkpoint tốt
# hoặc
/clear  # bắt đầu mới với context sạch

# Kết thúc session
# "Write session-notes.md with key decisions and next steps"
# Lần sau: "Read session-notes.md first"
```
