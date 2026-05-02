<!--
Sync Impact Report
Version change: none → 1.0.0
Modified principles: Layer Separation; Test-First; Minimal Dependencies; Simplicity First; CLI-Only Delivery
Added sections: Project Scope Constraints; Development Workflow
Templates requiring updates: .specify/templates/plan-template.md ✅ updated; .specify/templates/spec-template.md ✅ updated
Follow-up TODOs: none
-->

# Todo CLI Constitution

## Core Principles

### Layer Separation
비즈니스 로직은 사용자 인터페이스와 분리된 독립 레이어에서 구현한다. CLI 입력 처리, 출력 렌더링, 상태 저장과 업무 규칙은 분리하여 테스트 가능하고 재사용 가능한 서비스 계층을 만든다.

### Test-First
테스트 코드가 구현 코드보다 먼저 작성된다. 테스트가 없는 구현 코드는 허용하지 않으며, 모든 요구사항은 실패하는 테스트부터 시작하여 구현 전 검증되어야 한다.

### Minimal Dependencies
외부 패키지를 설치하기 전에 반드시 필요성을 검토한다. 불필요한 의존성은 추가하지 않으며, 표준 라이브러리로 해결할 수 있는 기능을 먼저 선택한다.

### Simplicity First
지금 당장 필요하지 않은 추상화 레이어는 만들지 않는다. 명확하고 직접적인 구현을 우선하고, 복잡한 설계는 실제 요구가 확인될 때까지 지연한다.

### CLI-Only Delivery
이 프로젝트는 터미널 CLI 도구로 구현한다. REST API 서버, GUI, 웹 인터페이스는 이 프로젝트의 범위 밖이며, 모든 사용자 경험은 명령줄과 텍스트 출력에 집중한다.

## Project Scope Constraints
- 프로젝트 범위는 터미널 기반 Todo 관리 CLI 도구로 제한된다.
- REST API, 웹 UI, 데스크톱 GUI, 모바일 앱은 금지된 구현 경로이다.
- 기능 설계와 문서화는 CLI 명령, 옵션, 표준 입출력 흐름을 중심으로 해야 한다.

## Development Workflow
- 모든 변경은 헌법 원칙과 일치해야 하며, PR과 코드 리뷰에서 CLI 범위, 레이어 분리, 테스트 우선, 최소 의존성, 단순함 우선을 검증한다.
- 핵심 구현 전에 테스트를 작성하고, 테스트가 실패하는 상태를 먼저 확보한 뒤에 코드를 작성한다.
- 새로운 라이브러리 또는 패키지 추가는 반드시 명시적인 필요성 평가와 대안 분석을 포함한다.

## Governance
- 이 헌법은 프로젝트의 기본 개발 원칙을 정의하며, 모든 설계와 구현은 이 헌법을 우선적으로 따라야 한다.
- 수정 또는 예외가 필요할 때는 문서화된 제안서를 작성하고 팀 합의를 받아야 한다.
- 버전 관리는 MAJOR.MINOR.PATCH 형식을 사용하며, 헌법의 구조나 핵심 원칙 변경 시 MAJOR를, 새로운 정책 추가 시 MINOR를, 용어 정리나 문안 개선 시 PATCH를 증가시킨다.
- 모든 PR은 적어도 한 명 이상의 리뷰어가 헌법 준수를 확인해야 하며, 테스트 우선 및 CLI 범위 위반이 없는지 확인해야 한다.

**Version**: 1.0.0 | **Ratified**: 2026-05-02 | **Last Amended**: 2026-05-02
