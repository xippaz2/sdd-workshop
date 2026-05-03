# Implementation Plan: Todo CLI App

**Branch**: `001-todo-cli-app` | **Date**: 2026-05-03 | **Spec**: `/specs/001-todo-cli-app/spec.md`
**Input**: Feature specification from `/specs/001-todo-cli-app/spec.md`

Summary

`specs/001-todo-cli-app/spec.md`의 핵심 요구 사항을 구현하기 위해 Python 3.12 기반 CLI Todo 앱을 작성합니다. 비즈니스 도메인은 `todo_lib/`에 두고, CLI 진입점은 `cli/`에 한정합니다. 데이터는 로컬 SQLite 파일에 저장하며 SQLAlchemy로 ORM 매핑을 단순하게 처리합니다. 테스트는 `pytest`와 `pytest-cov`로 선행 구현합니다.

## Technical Context

**Language/Version**: Python 3.12  
**Primary Dependencies**: typer, sqlalchemy  
**Storage**: SQLite 로컬 파일 기반 저장소  
**Testing**: pytest, pytest-cov  
**Target Platform**: Cross-platform terminal CLI  
**Project Type**: CLI application + library package  
**Performance Goals**: 1000개 Todo 항목 지원; 커맨드 응답 시간 <100ms; 앱 시작 시간 <1s  
**Constraints**: REST API/GUI 금지; 추상 repository 인터페이스 금지; 최소 의존성 유지; CLI 레이어와 비즈니스 레이어 분리  
**Scale/Scope**: 단일 사용자 로컬 Todo 관리, 단순 CRUD로 1개 테이블 모델

## Constitution Check

- CLI/터미널 전용: 스펙과 일치하며 REST API나 GUI는 배제한다.  
- 레이어 분리: `todo_lib/`에서 도메인 로직과 데이터 접근을 담당하고, `cli/`는 Typer로 입력을 파싱하고 `todo_lib`를 호출한다.  
- 테스트 우선: `tests/`를 먼저 추가하고, 실패하는 테스트를 확인한 뒤 구현을 작성한다.  
- 최소 의존성: runtime은 `typer`와 `sqlalchemy`만 사용하며, 추가 패키지를 도입하지 않는다.  
- 단순함 우선: `ITodoRepository` 같은 추상 인터페이스는 사용하지 않으며, 직접 `TodoDatabase`와 단순 함수/클래스 구현으로 처리한다.  

**추가 고려 사항**: constitution 5의 CLI 요구를 반영해 `--due`와 `--priority` 필드를 모델에 확장적으로 포함하지만, 핵심 스펙 동작은 `text`, `list`, `done` 토글 중심으로 유지한다.

## Project Structure

### Documentation (this feature)

```text
specs/001-todo-cli-app/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── cli-commands.md
└── tasks.md
```

### Source Code (repository root)

```text
todo_lib/
├── __init__.py
├── models.py
├── persistence.py
└── service.py

cli/
└── app.py

tests/
├── unit/
│   ├── test_todo_lib.py
│   └── test_cli.py
└── integration/
    └── test_end_to_end.py
```

**Structure Decision**: 단일 Python 패키지 `todo_lib`에서 도메인과 SQLite 저장소를 구현하고, `cli`는 오직 Typer 진입점으로만 역할을 수행한다. 테스트는 `tests/` 폴더에 두어 기능 검증과 통합 검증을 분리한다.

## Complexity Tracking

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| 없음 | - | - |
