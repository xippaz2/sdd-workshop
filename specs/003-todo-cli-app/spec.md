# Feature Specification: Todo CLI App

**Feature Branch**: `003-todo-cli-app`  
**Created**: 2026-05-02  
**Status**: Draft  
**Input**: User description: "CLI 기반의 TODO 관리 앱을 만들고 싶어요. 주요 기능: 1. TODO 항목 추가 - 제목(필수), 마감일(선택), 우선순위(선택) 2. 전체목록 조회 - 완료/미완료/우선순위로 필터링 가능 3. 항목 완료 처리 - 항목 ID로 완료 표시 4. 항목 삭제 - 항목 ID로 삭제 기술 스택은 아직 미정"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Todo 항목 추가 (Priority: P1)

사용자는 터미널에서 제목을 입력하여 새로운 Todo 항목을 추가할 수 있다.

**Why this priority**: Todo 앱의 핵심 기능이며, 다른 기능이 동작하려면 항목 생성이 먼저 필요하다.

**Independent Test**: `todo add "Buy groceries"` 명령 실행 후 항목이 생성되어 목록에 나타난다.

**Acceptance Scenarios**:

1. **Given** 명령줄이 준비된 상태, **When** `todo add "Buy groceries" --due 2026-05-05 --priority high` 입력, **Then** "Todo added: Buy groceries" 메시지가 출력되고 새 항목이 저장된다.
2. **Given** 제목만 입력된 상태, **When** `todo add "Read book"` 입력, **Then** 마감일과 우선순위가 선택 항목으로 남아 있는 새 Todo가 생성된다.
3. **Given** 제목이 비어 있거나 공백인 경우, **When** `todo add ""` 입력, **Then** 오류 메시지가 출력되고 항목이 생성되지 않는다.

---

### User Story 2 - Todo 목록 조회 (Priority: P2)

사용자는 모든 Todo 항목을 기본 목록으로 확인하고, 완료 상태 또는 우선순위로 필터링할 수 있다.

**Why this priority**: 사용자가 현재 작업 목록을 확인하고 우선순위와 상태별로 작업을 관리할 수 있도록 한다.

**Independent Test**: 여러 Todo를 추가한 뒤 `todo list`, `todo list --status incomplete`, `todo list --priority high` 명령으로 결과를 확인한다.

**Acceptance Scenarios**:

1. **Given** Todo 항목이 존재, **When** `todo list` 입력, **Then** 모든 항목이 ID, 제목, 상태, 마감일, 우선순위로 표시된다.
2. **Given** 완료된 항목이 포함된 상태, **When** `todo list --status complete` 입력, **Then** 완료된 항목만 표시된다.
3. **Given** 여러 우선순위 항목이 존재, **When** `todo list --priority high` 입력, **Then** 우선순위가 high인 항목만 표시된다.

---

### User Story 3 - Todo 완료 처리 및 삭제 (Priority: P3)

사용자는 항목 ID로 Todo를 완료 처리하거나 삭제할 수 있다.

**Why this priority**: Todo 리스트를 실제로 관리하려면 항목을 완료 처리하고 필요 없는 항목을 제거할 수 있어야 한다.

**Independent Test**: `todo done 2` 또는 `todo delete 2` 명령을 실행하여 지정된 항목의 상태 또는 존재 여부를 확인한다.

**Acceptance Scenarios**:

1. **Given** 미완료 Todo 항목이 존재, **When** `todo done 1` 입력, **Then** 항목 1이 완료 상태로 표시된다.
2. **Given** 존재하는 항목이 있을 때, **When** `todo delete 1` 입력, **Then** 항목 1이 목록에서 삭제된다.
3. **Given** 존재하지 않는 ID를 입력한 경우, **When** `todo done 999` 또는 `todo delete 999` 입력, **Then** 적절한 오류 메시지가 출력되고 다른 항목은 영향을 받지 않는다.

### Edge Cases

- 제목 없이 Todo를 추가하려고 할 때 사용자에게 명확한 오류를 보여준다.
- 존재하지 않는 ID로 완료 처리 또는 삭제 요청 시 실패 메시지를 제공한다.
- 저장 파일이 없거나 손상된 경우 기본 상태로 복구하거나 오류를 안내한다.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: 시스템은 CLI 명령으로 Todo 항목을 추가할 수 있어야 한다.
- **FR-002**: Todo 항목 추가 시 제목은 필수이며, 마감일과 우선순위는 선택 사항이어야 한다.
- **FR-003**: 사용자는 전체 Todo 목록을 조회할 수 있어야 한다.
- **FR-004**: 사용자는 완료 상태(`complete`, `incomplete`) 또는 우선순위(`high`, `medium`, `low`)로 목록을 필터링할 수 있어야 한다.
- **FR-005**: 사용자는 항목 ID로 Todo를 완료 처리할 수 있어야 한다.
- **FR-006**: 사용자는 항목 ID로 Todo를 삭제할 수 있어야 한다.
- **FR-007**: 시스템은 Todo 항목을 로컬 파일에 영구 저장해야 한다.
- **FR-008**: 시스템은 오류 상황에서 사용자에게 명확한 메시지를 제공해야 한다.

### Key Entities *(include if feature involves data)*

- **Todo**: 제목(text), 생성 시각(created_at), 마감일(due_date, 선택), 우선순위(priority, 선택), 완료 상태(is_complete), 고유 ID(id)

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 사용자가 5초 이내에 Todo 항목을 추가하거나 삭제할 수 있다.
- **SC-002**: 사용자는 10개 이상의 Todo 항목을 `list` 명령으로 2초 이내에 확인할 수 있다.
- **SC-003**: 95%의 경우에 잘못된 ID 입력 시 명확한 오류 메시지가 제공된다.
- **SC-004**: Todo 항목 추가 시 제목 누락 오류는 항상 사용자에게 명확히 안내된다.

## Assumptions

- 이 기능은 터미널 기반 CLI 도구로 구현되며 REST API, GUI, 웹 인터페이스는 범위 밖이다.
- Todo 데이터는 로컬 파일(예: JSON 또는 간단한 텍스트 저장소)에 저장된다.
- 우선순위 값은 high/medium/low 세 가지로 제한된다.
- 사용자 인증이나 멀티 유저 지원은 현재 버전에서 포함되지 않는다.
