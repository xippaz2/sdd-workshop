# Research: Todo CLI App

## Decision

- 실행 환경은 Python 3.12로 고정한다.  
- CLI 구현은 Typer를 사용한다.  
- 로컬 데이터 저장은 SQLite 파일 기반을 선택하고 SQLAlchemy ORM을 사용해 간결하게 매핑한다.  
- 테스트는 pytest와 pytest-cov로 작성한다.

## Rationale

- `typer`는 Python CLI 구현을 간결하게 하며, 선언적 옵션과 자동 도움말을 제공해 CLI 도구 요건에 적합하다.  
- SQLite는 로컬 파일 기반 저장소로 서버 없이 실행되며, 스펙에서 요구하는 영구 저장과 1000개 이상 항목 처리에 충분하다.  
- SQLAlchemy는 ORM 매핑을 제공하므로 데이터 모델 정의와 쿼리 구현을 명시적으로 관리할 수 있다. 사용 가능한 최저 의존성 범위 내에서 유지된다.  
- `pytest`와 `pytest-cov`는 테스트 우선 원칙에 부합하며, CLI와 라이브러리 로직을 동시에 검증할 수 있다.

## Alternatives Considered

1. JSON 파일 저장  
   - 장점: 구현이 매우 단순하다.  
   - 단점: 데이터 무결성, 동시성, 필터링 쿼리 구현이 취약해지고 스케일링이 어려움.  
   - 판단: SQLite가 더 안정적이고 명확한 로컬 데이터 저장 방식이다.

2. raw `sqlite3` 모듈 사용  
   - 장점: 추가 의존성 없이 SQL 사용 가능.  
   - 단점: 매핑과 스키마 관리를 직접 작성해야 하며, 타입 검증이 분산된다.  
   - 판단: SQLAlchemy가 허용된 의존성 안에서 코드 명료성을 높인다.

3. 메모리 기반 저장  
   - 장점: 가장 간단함.  
   - 단점: 영구 저장 요건을 충족하지 못함.  
   - 판단: 스펙과 맞지 않으므로 배제.

## Decision Summary

- 핵심 스펙은 `add`, `list`, `done` 토글 및 오류 메시지 처리에 집중한다.  
- constitution의 CLI 확장 요구를 반영해 `--due`와 `--priority` 옵션을 수용하도록 설계한다.  
- `todo_lib`는 도메인 모델과 데이터 저장을 담당하고, `cli`는 사용자 입력/출력에만 책임을 둔다.
