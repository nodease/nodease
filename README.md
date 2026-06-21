# Nodease

Agent + MCP 기반 workflow automation MVP 스켈레톤입니다.

현재 저장소는 실행 코드가 아니라 폴더 구조와 구현 계획만 포함합니다. 런타임 코드, 패키지 설정, Docker Compose, DB migration은 `docs/plan.md`의 마일스톤 순서에 따라 추가합니다.

## 구조

- `frontend`: 프론트엔드 영역입니다.
- `backend/gateway`: HTTP API, 인증, tenant 권한, frontend-facing contract를 담당합니다.
- `backend/workflow_engine`: 저장된 workflow 실행과 node run orchestration을 담당합니다.
- `backend/agent_service`: 자연어 요청을 workflow draft로 변환하는 Agent 영역입니다.
- `backend/mcp_server`: 외부 MCP discovery, MCP Tool Node 경계, Nodease MCP endpoint를 담당합니다.
- `backend/log_system`: workflow, node, Agent, MCP, sandbox, audit log를 담당합니다.
- `backend/shared`: schema, DB model, node catalog, graph validation, permission, credential helper를 담당합니다.
- `sandbox`: 사용자 코드를 격리된 disposable container에서 실행하는 별도 서비스 영역입니다.
- `db`: migration, seed, init SQL, schema 문서를 관리합니다.
- `docker`: Compose, Dockerfile, sandbox runtime image 등 로컬 실행 자산을 관리합니다.
- `docs`: 전체 제품 spec과 구현 plan을 관리합니다.
- `agent.md`: 프로젝트 작업 규칙을 정의합니다.

## 문서

- `docs/spec.md`: 전체 MVP 스펙
- `docs/plan.md`: 전체 구현 마일스톤
- 각 구현 폴더의 `docs/spec.md`: 해당 모듈의 구현 책임과 기술 스택
- 각 구현 폴더의 `docs/plan.md`: 해당 모듈의 구현 순서와 검증 기준

## 현재 상태

- 스켈레톤 구조만 구성되어 있습니다.
- 실행 가능한 backend/frontend/sandbox 코드는 아직 없습니다.
- Docker Compose와 DB migration도 아직 없습니다.
- 기능 구현은 `docs/plan.md` 순서대로 진행합니다.
