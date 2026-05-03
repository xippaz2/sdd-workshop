# Data Model: Todo CLI App

## Entity: Todo

- **id**: integer primary key, auto-increment  
- **text**: string, non-empty  
- **created_at**: datetime, 생성 시 자동 설정  
- **done**: boolean, 기본값 `false`  
- **due_date**: optional date, YYYY-MM-DD 형식  
- **priority**: optional enum, 값은 `high`, `medium`, `low`

## Validation Rules

- `text`는 빈 문자열이 될 수 없다.  
- `due_date`가 주어지면 유효한 `YYYY-MM-DD` 형식이어야 한다.  
- `priority`가 주어지면 `high`, `medium`, `low` 중 하나여야 한다.  
- `done`은 `todo done <id>` 명령으로 토글 가능해야 한다.

## Relationships

- 이 기능은 단일 엔티티 `Todo`만 사용하며, 다른 엔티티와의 관계는 없다.

## State Transitions

- `pending` → `done`  
- `done` → `pending` (same command `todo done <id>` 재실행 시 토글)

## Storage Model

- SQLite 테이블 `todos`  
- SQLAlchemy 모델을 사용하여 필드를 매핑한다.  
- `id`는 데이터베이스 자동 증가를 사용해 생성한다.
