# Nodease MVP Plan

이 계획은 `docs/spec.md`의 폴더별 책임을 실제 구현 순서로 나눈다.

## M0. Skeleton 정리

Priority: P0

구현:

- `frontend` 생성
- `backend/gateway` 생성
- `backend/workflow_engine` 생성
- `backend/agent_service` 생성
- `backend/mcp_server` 생성
- `backend/log_system` 생성
- `backend/shared` 생성
- `sandbox` 생성
- `db` 생성
- `docker` 생성
- 각 폴더에 README와 `.gitkeep`를 둔다.
- 구현 대상 폴더마다 `docs/spec.md`와 `docs/plan.md`를 둔다.

검증:

- 구현 코드가 없어야 한다.
- 폴더 책임이 README와 `docs/spec.md`에 설명되어 있어야 한다.
- 모듈별 상세 문서가 모두 존재해야 한다.

## M1. Shared Contract Foundation

Priority: P0

구현:

- `backend/shared`에 공통 schema 위치를 만든다.
- workflow graph schema를 정의한다.
- Graph Patch schema를 정의한다.
- internal node catalog 구조를 정의한다.
- permission helper 경계를 정의한다.
- credential encryption helper 경계를 정의한다.

기술:

- Pydantic v2
- SQLAlchemy 2
- cryptography
- pytest

검증:

- gateway, workflow_engine, agent_service, mcp_server가 같은 schema를 import할 수 있어야 한다.
- unknown node type을 거절할 수 있어야 한다.
- execution handler는 shared에 없어야 한다.

## M2. DB + Auth Foundation

Priority: P0

구현:

- `db/migrations`에 Alembic 기반 migration을 둔다.
- users, tenants, memberships, sessions를 만든다.
- password login을 만든다.
- JWT session을 만든다.
- tenant permission check를 만든다.

기술:

- PostgreSQL 17
- Alembic
- SQLAlchemy 2
- FastAPI
- pwdlib[argon2]
- JWT/OAuth

검증:

- 사용자가 가입/로그인할 수 있어야 한다.
- 요청마다 user와 tenant context가 확인되어야 한다.
- 권한 없는 tenant resource 접근이 거절되어야 한다.

## M3. Gateway MVP

Priority: P0

구현:

- `backend/gateway`에 HTTP API 서버를 만든다.
- auth route를 만든다.
- workflow CRUD route를 만든다.
- workflow run 요청 route를 만든다.
- Agent draft 요청 route를 만든다.
- MCP connection 관리 route를 만든다.

기술:

- FastAPI
- Pydantic v2
- SQLAlchemy 2
- httpx
- pytest

검증:

- frontend가 호출할 API contract가 고정되어야 한다.
- gateway는 실행 로직을 직접 갖지 않아야 한다.
- workflow 실행은 workflow_engine에 위임되어야 한다.

## M4. Workflow 저장

Priority: P0

구현:

- workflows 테이블을 만든다.
- workflow_versions 테이블을 만든다.
- graph JSON 저장을 만든다.
- 저장 전 graph validation을 수행한다.
- frontend에서 workflow를 저장/불러온다.

기술:

- PostgreSQL
- SQLAlchemy 2
- FastAPI
- React Flow
- Zustand

검증:

- 사용자가 workflow draft를 만들고 다시 열 수 있어야 한다.
- invalid graph는 저장되지 않아야 한다.

## M5. Workflow Engine 실행

Priority: P0

구현:

- `backend/workflow_engine`을 Celery worker로 만든다.
- workflow_runs 테이블을 만든다.
- node_run_logs 테이블을 만든다.
- start, answer, llm placeholder, mcp placeholder node를 실행한다.
- run status를 기록한다.

기술:

- Celery 5
- Redis 7.4
- SQLAlchemy 2
- Pydantic v2

검증:

- gateway가 run을 enqueue할 수 있어야 한다.
- workflow_engine이 run을 처리하고 status를 기록해야 한다.
- node output이 다음 node input으로 전달되어야 한다.

## M6. Frontend MVP

Priority: P0

구현:

- 로그인 화면을 만든다.
- workflow 목록 화면을 만든다.
- React Flow editor를 만든다.
- node palette를 만든다.
- workflow 저장/실행 버튼을 만든다.
- run log 조회 화면을 만든다.

기술:

- Next.js 16
- React 19
- TypeScript
- React Flow
- Tailwind CSS
- Zustand
- Vitest

검증:

- 로그인 후 workflow 목록에 접근할 수 있어야 한다.
- workflow를 저장하고 다시 열 수 있어야 한다.
- 실행 요청과 로그 조회가 가능해야 한다.

## M7. Log System

Priority: P1

구현:

- `backend/log_system`을 만든다.
- workflow run log를 저장한다.
- node run log를 저장한다.
- Agent decision log를 저장한다.
- MCP tool call log를 저장한다.
- sandbox execution log를 저장한다.

기술:

- PostgreSQL
- SQLAlchemy 2
- structlog 또는 표준 logging

검증:

- workflow 실행 이력이 조회 가능해야 한다.
- 실패한 node의 입력, 출력, 에러가 추적 가능해야 한다.
- secret은 log에 남지 않아야 한다.

## M8. Agent Service

Priority: P1

구현:

- `backend/agent_service`를 만든다.
- 자연어 요청을 받는다.
- internal node catalog를 읽는다.
- MCP tool catalog를 읽는다.
- Graph Patch를 만든다.
- 위험한 tool/node를 표시한다.
- 직접 저장하지 않고 preview 응답만 반환한다.

기술:

- LangGraph
- LiteLLM
- MCP Python SDK
- Pydantic v2
- httpx

검증:

- Agent 요청이 Graph Patch를 반환해야 한다.
- Patch는 자동 저장되지 않아야 한다.
- frontend가 Patch preview를 보여줄 수 있어야 한다.

## M9. MCP Server

Priority: P1

구현:

- `backend/mcp_server`를 만든다.
- 외부 MCP server를 등록한다.
- MCP tool list를 조회한다.
- tool schema snapshot을 저장한다.
- MCP Tool Node 실행 경계를 만든다.
- 내부 기능 일부를 MCP endpoint로 노출한다.

기술:

- MCP Python SDK
- Streamable HTTP
- FastAPI
- httpx
- Pydantic v2

검증:

- 외부 MCP tool 목록을 조회할 수 있어야 한다.
- MCP Tool Node가 schema snapshot을 저장해야 한다.
- 인증 없는 MCP 요청은 거절되어야 한다.

## M10. Sandbox

Priority: P1

구현:

- `sandbox`를 별도 서버로 만든다.
- disposable Docker execution container를 만든다.
- timeout, CPU, memory, pids 제한을 적용한다.
- read-only filesystem을 적용한다.
- network policy를 적용한다.
- 실행 후 container를 정리한다.

기술:

- FastAPI
- Docker isolated container
- Docker SDK 또는 Docker CLI boundary
- pytest

검증:

- 사용자 코드는 sandbox 밖에서 실행되지 않아야 한다.
- timeout과 resource limit이 동작해야 한다.
- 실행 결과와 audit log가 저장되어야 한다.

## M11. Docker Local Runtime

Priority: P2

구현:

- `docker`에 Compose 설정을 만든다.
- frontend service를 만든다.
- gateway service를 만든다.
- workflow_engine service를 만든다.
- agent_service service를 만든다.
- mcp_server service를 만든다.
- log_system service를 만든다.
- sandbox service를 만든다.
- postgres service를 만든다.
- redis service를 만든다.

기술:

- Docker Compose
- Dockerfile
- PostgreSQL 17
- Redis 7.4

검증:

- `docker compose config`가 통과해야 한다.
- 각 서비스가 이름으로 통신 가능해야 한다.
- sandbox는 별도 네트워크 정책을 가져야 한다.

## M12. Release Hardening

Priority: P2

구현:

- backend pytest를 추가한다.
- frontend Vitest를 추가한다.
- 주요 API contract test를 추가한다.
- secret logging 방지 검사를 추가한다.
- threat model 문서를 추가한다.

검증:

- backend test가 통과해야 한다.
- frontend test가 통과해야 한다.
- workflow graph와 log에 secret이 없어야 한다.
- MVP 범위를 벗어난 marketplace, billing, enterprise RBAC, Kubernetes는 추가하지 않는다.
