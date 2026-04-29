# Project: [Tên Project]
<!-- TEMPLATE: Copy → điền theo project thực tế
     Đặt file này ở root directory của project.
     Giữ < 5.000 token | Load thêm: @docs/api.md, @docs/testing.md -->

## Tech Stack
[Điền theo project, vd:]
- Language: Python 3.11 / Node.js 20 / Go 1.22
- Framework: FastAPI / Express / Gin
- Database: PostgreSQL 15 / MySQL 8 / MongoDB
- Cache: Redis 7
- Container: Docker + docker-compose
- CI/CD: GitHub Actions / GitLab CI

## Architecture Overview
[1 đoạn mô tả ngắn kiến trúc — monolith / microservices / serverless]
[Hoặc link: @docs/architecture.md]

## Conventions
- Naming: [snake_case / camelCase] cho variables, [PascalCase] cho classes
- Imports: [absolute / relative] — group: stdlib → third-party → local
- Language: [Vietnamese comments, English code / all English]
- Tests: [pytest / jest], coverage > [N]%, integration tests [hit real DB / use fixtures]

## Environment Setup
```bash
# Clone và setup
git clone [repo-url]
cd [project-name]
cp .env.example .env  # fill in your values

# Install
[pip install -r requirements.txt / npm install]

# Run locally
[python main.py / npm run dev]

# Run tests
[pytest / npm test]
```

## Key Files
- Entry point: `[main.py / index.js / cmd/main.go]`
- Config: `[config.py / config.js / config/]`
- Models: `[models/ / src/models/]`
- Tests: `[tests/ / __tests__/]`

## Known Issues / Workarounds
- [Bug/limitation 1]: Workaround là [...]
- [Bug/limitation 2]: Workaround là [...]

## Current TODOs
- [ ] [Feature / refactor đang làm]
- [ ] [Next task]

## Do NOT
- KHÔNG push trực tiếp lên `main` / `production`
- KHÔNG hardcode secrets — dùng environment variables
- KHÔNG modify `[file/folder nhạy cảm]` mà không có approval
