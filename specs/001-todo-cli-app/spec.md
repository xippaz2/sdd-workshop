# Feature Specification: Todo CLI App

**Feature Branch**: `001-todo-cli-app`  
**Created**: 2026-05-02  
**Status**: Draft  
**Input**: User description: "이 프로젝트는 CLI 기반으로 Todo 관리앱을 만듭니다. 터미널에서 사용하는 생산성 관리 도구로 REST API나 GUI는 프로젝트의 범위 밖입니다."

## Clarifications

### Session 2026-05-03

- Q: JSON 파일의 파일명과 경로는 무엇으로 할까요? → A: 현재 디렉토리에 todos.json 파일로 저장
- Q: Todo ID는 어떻게 생성할까요? → A: 1부터 시작하는 순차 정수
- Q: 완료된 Todo는 목록에서 어떻게 별도 표시할까요? → A: 목록 끝에 [DONE] 접두사로 표시
- Q: 에지 케이스에 대한 구체적인 오류 메시지를 어떻게 할까요? → A: 빈 문자열: 'Todo 텍스트가 비어있음'; 잘못된 ID: '존재하지 않는 Todo ID'; 파일 손상: '데이터 파일이 손상됨'
- Q: 'done' 명령이 완료된 Todo를 다시 미완료로 변경할 수 있나요? → A: 예, 완료 상태를 토글할 수 있음

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Todo 추가 (Priority: P1)

사용자가 터미널에서 새로운 Todo 항목을 추가할 수 있다.

**Why this priority**: Todo 앱의 핵심 기능으로, 가장 기본적인 작업이다.

**Independent Test**: 명령줄에서 `todo add "Buy milk"`를 실행하면 Todo가 추가되고, 목록에 나타난다.

**Acceptance Scenarios**:

1. **Given** 터미널이 실행 중, **When** `todo add "Buy milk"` 입력, **Then** "Todo added: Buy milk" 메시지 출력
2. **Given** 빈 Todo 목록, **When** Todo 추가 후 목록 조회, **Then** 추가된 Todo가 목록에 표시됨

---

### User Story 2 - Todo 목록 보기 (Priority: P2)

사용자가 모든 Todo 항목을 목록으로 볼 수 있다.

**Why this priority**: 추가된 Todo를 확인하는 필수 기능이다.

**Independent Test**: 여러 Todo를 추가한 후 `todo list` 명령으로 모든 항목이 표시된다.

**Acceptance Scenarios**:

1. **Given** Todo 항목이 존재, **When** `todo list` 입력, **Then** 모든 Todo가 번호와 함께 표시됨
2. **Given** 빈 목록, **When** `todo list` 입력, **Then** "No todos found" 메시지 출력

---

### User Story 3 - Todo 완료 표시 (Priority: P3)

사용자가 Todo 항목을 완료로 표시하거나 미완료로 변경할 수 있다.

**Why this priority**: Todo 관리의 완결 기능으로, 생산성 향상에 기여한다.

**Independent Test**: Todo를 완료 표시하면 목록에서 완료 상태로 변경된다.

**Acceptance Scenarios**:

1. **Given** 미완료 Todo 존재, **When** `todo done 1` 입력, **Then** 첫 번째 Todo가 완료로 표시됨
2. **Given** 완료된 Todo, **When** 목록 조회, **Then** 완료된 항목은 목록 끝에 [DONE] 접두사로 표시됨
3. **Given** 완료된 Todo 존재, **When** `todo done 1` 입력, **Then** 첫 번째 Todo가 미완료로 변경됨

### Edge Cases

- 빈 문자열 Todo 추가 시도: 'Todo 텍스트가 비어있음' 오류 메시지 출력
- 존재하지 않는 ID로 완료 표시: '존재하지 않는 Todo ID' 오류 메시지 출력
- 저장 파일이 손상된 경우: '데이터 파일이 손상됨' 오류 메시지 출력

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: 시스템은 CLI 명령을 통해 Todo 항목을 추가할 수 있어야 한다
- **FR-002**: 시스템은 모든 Todo 항목을 목록으로 표시할 수 있어야 한다  
- **FR-003**: 시스템은 Todo 항목을 완료로 표시할 수 있어야 한다
- **FR-004**: 시스템은 Todo 데이터를 파일에 영구 저장해야 한다
- **FR-005**: 시스템은 사용자 친화적인 오류 메시지를 출력해야 한다

### Key Entities *(include if feature involves data)*

- **Todo**: 텍스트 내용, 생성 시간, 완료 상태, 1부터 시작하는 순차 정수 ID를 가짐

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 사용자가 10초 이내에 Todo를 추가하고 확인할 수 있다
- **SC-002**: 시스템이 1000개 Todo 항목을 처리할 수 있다
- **SC-003**: 95%의 사용자가 주요 명령을 성공적으로 사용할 수 있다
- **SC-004**: 시스템 시작 시간이 1초 이내이다

## Assumptions

- This feature is implemented as a terminal CLI tool and must not depend on REST API, GUI, or web interface components.
- Todo 데이터는 현재 디렉토리의 todos.json 파일에 저장된다
- 우선순위나 카테고리는 지원하지 않는다
- 다중 사용자는 고려하지 않는다