# Claude Code — Slash Commands Cheatsheet
> Claude Code v2.1+ | Tháng 4/2026

---

## LỆNH HAY DÙNG NHẤT

| Lệnh | Tác dụng | Khi nào dùng |
|------|----------|--------------|
| `/plan` | Bật Plan Mode — Claude phân tích trước, không code ngay | Trước mọi task phức tạp |
| `/compact` | Tóm tắt conversation, giải phóng context window | Session dài > 50 lượt |
| `/clear` | Xóa conversation, bắt đầu session mới | Task hoàn toàn khác |
| `/model` | Chuyển model (haiku/sonnet/opus/opusplan) | Tiết kiệm token hoặc cần sức mạnh cao |
| `/cost` | Xem chi phí token session hiện tại | Kiểm tra budget |
| `#` | Cập nhật memory ngay lập tức | Thêm quy tắc/context mới vào session |
| `/rewind N` | Quay lại N lượt trước | Khi Claude đi sai hướng |

---

## MODEL & EFFORT

```bash
/model haiku        # Nhanh, rẻ — task đơn giản (tóm tắt, dịch, phân loại)
/model sonnet       # Cân bằng — default cho hầu hết tasks
/model opus         # Mạnh nhất — phân tích phức tạp, lập kế hoạch dài
/model opusplan     # Auto: Opus khi plan, Sonnet khi execute (tiết kiệm)

/effort low         # Thinking tối thiểu
/effort medium      # Default — cân bằng (80% cases)
/effort high        # Reasoning sâu — task phức tạp
/effort max         # Extended thinking — dùng tiết kiệm (rất đắt token)
```

---

## MEMORY & CONTEXT

```bash
# Cập nhật memory nhanh trong chat
# Python version phải là 3.11, không dùng 3.12
# Database là PostgreSQL 15, không phải MySQL
# [Quy tắc gì đó]

/init               # Tạo CLAUDE.md tự động từ project hiện tại
```

**Quản lý context:**
```bash
/compact            # Tóm tắt + giải phóng context window
                    # TIP: Trước khi /compact, nói:
                    # "Before compacting, preserve: (1) files modified (2) decisions (3) next TODO"

/clear              # Xóa hoàn toàn — bắt đầu mới
```

---

## NAVIGATION & UNDO

```bash
/rewind             # Xem danh sách checkpoints (auto-saved sau mỗi prompt)
/rewind 1           # Quay lại 1 lượt trước
/rewind 5           # Quay lại 5 lượt

# Keyboard:
# Esc + Esc         # Mở rewind menu (nhanh hơn)
```

---

## SKILLS (Custom Commands)

```bash
/build-prompt       # Xây prompt chuẩn từ đầu (hỏi → sinh → refine)
/review             # Code review theo checklist
/deal-brief         # Sales: brief trước cuộc họp
/repurpose          # Marketing: 1 bài → 4 format
/synthesize         # BA: tổng hợp transcript
/dq-check           # Data: data quality check
/recon              # Finance: variance analysis
/onboard            # HR: tạo onboarding kit

# Xem tất cả skills:
/skills
```

---

## SCHEDULING & AUTOMATION

```bash
/loop               # Lặp lại task định kỳ (trong session)
                    # vd: /loop 5m check build status
                    # vd: /loop watch changes in /logs

/schedule           # Tạo scheduled agent chạy theo cron (remote)
                    # vd: /schedule daily report at 8am
```

---

## SUBAGENTS & ISOLATION

```bash
# Trong prompt (không phải slash command):
"Use subagents to investigate X in parallel"
"Use the Explore agent to search for..."
"Use the Plan agent to design..."

# Isolation worktree (làm việc trên branch riêng):
# Trong SKILL.md: thêm "context: fork"
# Hoặc: claude -w (mở session trên git worktree riêng)
```

---

## SESSION MANAGEMENT

```bash
claude              # Bắt đầu session mới tương tác
claude -c           # Tiếp tục session gần nhất
claude -r "tên"     # Resume session đã đặt tên
claude -p "query"   # Chạy 1 câu hỏi, thoát (non-interactive)
claude -w           # Mở trên git worktree mới

# Pipe input:
cat error.log | claude -p "tìm root cause"
cat file.py | claude -p "review security"
```

---

## OUTPUT FORMATS

```bash
claude -p "query" --output-format json      # JSON output
claude -p "query" --output-format markdown  # Markdown
claude -p "query" --output-format text      # Plain text

# Dùng trong scripts:
claude -p "analyze" --output-format json | jq '.result'
```

---

## MCP SERVERS (Model Context Protocol)

```bash
# Cài MCP server:
claude mcp add --transport http github https://api.github.com/mcp
claude mcp add --transport stdio postgres -- npx @modelcontextprotocol/server-postgres postgresql://...

# List MCP servers đã cài:
/mcp

# MCP tools tự động thành slash commands:
/mcp__github__list_prs
/mcp__github__create_issue
```

---

## PERMISSION MODES

```bash
Shift+Tab           # Cycle qua các modes:
                    # default → acceptEdits → plan → auto → dontAsk

--permission-mode plan         # Chỉ đọc + lập kế hoạch
--permission-mode acceptEdits  # Auto-accept file edits
--permission-mode auto         # Autonomous với safety classifier
```

---

## ENVIRONMENT VARIABLES (settings.json)

| Variable | Default | Khuyến nghị | Tác dụng |
|----------|---------|-------------|----------|
| `MAX_THINKING_TOKENS` | 31,999 | 10,000 | Giảm extended thinking cost |
| `CLAUDE_CODE_SUBAGENT_MODEL` | model chính | `claude-haiku-4-5-20251001` | Subagents dùng Haiku |
| `DISABLE_NON_ESSENTIAL_MODEL_CALLS` | 0 | 1 | Tắt background model calls |
| `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` | 95% | 70% | Compact sớm hơn |
| `DISABLE_AUTO_COMPACT` | 0 | 1 (tùy) | Tắt auto-compact |
| `CLAUDE_CODE_DISABLE_AUTO_MEMORY` | 0 | 1 (tùy) | Tắt auto memory |

---

## QUICK REFERENCE: 10 LỆNH THIẾT YẾU

```
1. /plan          — Phân tích trước, không làm ngay
2. /compact       — Giải phóng context khi session dài
3. /model opusplan — Opus khi plan, Sonnet khi execute
4. # [quy tắc]   — Cập nhật memory ngay
5. /rewind N      — Undo N lượt
6. /clear         — Bắt đầu lại hoàn toàn
7. /cost          — Kiểm tra token đã dùng
8. /effort medium — Đặt mức thinking (default)
9. /loop          — Lặp task định kỳ
10. /btw          — Hỏi nhanh không vào history
```
