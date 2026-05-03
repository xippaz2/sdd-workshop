# Quickstart: Todo CLI App

## 환경 설정

1. Python 3.12가 설치되어 있어야 합니다.  
2. `uv` 패키지 관리자를 사용해 의존성을 설치합니다:

```powershell
uv sync install typer sqlalchemy pytest pytest-cov
```

3. 패키지를 설치한 후 테스트를 실행합니다:

```powershell
uv run python -m pytest --cov=todo_lib tests
```

## 실행 예시

### Todo 추가

```powershell
uv run python -m cli.app add "Buy milk" --due 2026-05-10 --priority high
```

### Todo 목록 보기

```powershell
uv run python -m cli.app list
```

### 완료 상태 필터링

```powershell
uv run python -m cli.app list --filter done
uv run python -m cli.app list --filter pending
```

### 우선순위 필터링

```powershell
uv run python -m cli.app list --priority high
```

### Todo 완료 토글

```powershell
uv run python -m cli.app done 1
```

### Todo 삭제

```powershell
uv run python -m cli.app delete 1
```

## 데이터 위치

- 기본 SQLite 데이터 파일은 프로젝트 루트에 `todos.db`로 저장됩니다.
