# CLI Commands Contract: Todo CLI App

## Command: add

```text
todo add "<title>" [--due YYYY-MM-DD] [--priority high|medium|low]
```

- `title`: 필수 문자열  
- `--due`: 선택적 마감일  
- `--priority`: 선택적 우선순위  

### Expected output

- 성공: `Todo added: <title>`  
- 오류: 
  - `Todo 텍스트가 비어있음`  
  - `유효하지 않은 우선순위입니다`  
  - `유효하지 않은 날짜 형식입니다`  

## Command: list

```text
todo list [--filter done|pending] [--priority high|medium|low]
```

### Expected output

- Todo가 있을 때:
  - 각 항목은 `ID. [DONE] <text> (due: YYYY-MM-DD, priority: high)` 형식으로 표시
- Todo가 없을 때:
  - `No todos found`

## Command: done

```text
todo done <id>
```

- `id`: 정수 식별자

### Expected output

- 완료로 변경 시: `Todo marked as done: <text>`  
- 미완료로 변경 시: `Todo marked as pending: <text>`  
- 오류: `존재하지 않는 Todo ID`

## Command: delete

```text
todo delete <id>
```

### Expected output

- 성공: `Todo deleted: <text>`  
- 오류: `존재하지 않는 Todo ID`

## Error contract

- 빈 제목: `Todo 텍스트가 비어있음`  
- 잘못된 ID: `존재하지 않는 Todo ID`  
- 손상된 데이터베이스: `데이터 파일이 손상됨`
