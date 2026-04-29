# Coding Conventions
<!-- Điều chỉnh theo tech stack thực tế của công ty bạn -->

## Stack mặc định
<!-- Ví dụ — thay bằng stack thực tế:
- Backend: [Python 3.11 / Node.js / Go / Java / ...]
- Database: [PostgreSQL / MySQL / MongoDB / ...]
- Cache: [Redis / Memcached / ...]
- Container: [Docker / Kubernetes / ...]
- Testing: [pytest / Jest / JUnit / ...]
-->
- Backend: [ngôn ngữ + framework]
- Database: [database chính]
- Testing: [framework], coverage > 80%

## Naming Conventions

### Variables & Functions
```
# snake_case (Python) / camelCase (JS/Java) — chọn 1 nhất quán
def calculate_monthly_revenue(amount: float, month: int) -> float:
    ...
```

### Classes
```
# PascalCase
class ReportGenerator:
    ...
```

### Constants
```
# SCREAMING_SNAKE_CASE
MAX_RETRY_COUNT = 3
DEFAULT_TIMEOUT_SECONDS = 30
```

### Private / Internal
```
# prefix _ cho private
def _validate_input(data: dict) -> bool:
    ...
```

## Import Order (Python example)
```python
# 1. Standard library
import os
from datetime import date

# 2. Third-party
import pandas as pd

# 3. Local
from app.models import User
```

## Type Hints (bắt buộc cho public functions)
```python
def get_report(
    report_id: int,
    start_date: date,
    end_date: date
) -> dict:
    ...
```

## Error Handling
```python
# Dùng specific exceptions, không bare except
try:
    result = fetch_data(id)
except ValueError as e:
    logger.error(f"Invalid input {id}: {e}")
    raise
except ConnectionError as e:
    logger.error(f"Service unavailable: {e}")
    raise
```

## API Conventions
```
# REST style, lowercase, hyphen
GET  /api/v1/reports/{id}
POST /api/v1/reports/batch
DELETE /api/v1/cache/{key}

# Response models: luôn explicit, có status + data + error
```

## Testing
```python
# test_[function]_[scenario]
def test_calculate_revenue_positive():
    ...

def test_calculate_revenue_zero_amount():
    ...

# Integration tests: hit real DB (không mock DB)
# Unit tests: mock external calls (API, third-party)
```

## Git Workflow
- Branch: `feat/`, `fix/`, `chore/`, `docs/`
- Commit message: imperative mood, tiếng Anh
  - `feat: add monthly report endpoint`
  - `fix: handle null value in revenue calculation`
- PR: require 1 reviewer, pass CI, coverage không giảm
- KHÔNG push trực tiếp lên `main`

## Security Rules
- Không hardcode secrets/credentials trong code
- Dùng environment variables: `os.getenv("DB_PASSWORD")`
- Không log PII (email, phone, tên khách hàng)
- SQL: dùng parameterized queries, không string format
