# Nodease MVP Spec

## 기준

Nodease는 MVP 최소 기준으로 삼고, 상위 구조만 `frontend / backend / sandbox / db`로 단순화한다.

## 목표

사용자가 시각적으로 자동화 workflow를 만들고, Agent가 자연어 요청을 저장 가능한 workflow 초안으로 변환하는 MVP를 만든다.

MVP 필수 범위:

- 로그인, 사용자, tenant, 권한
- workflow 생성, 저장, 버전, 실행
- Agent 기반 workflow draft 생성
- 내부 Node Catalog
- 외부 MCP tool 조회와 MCP Tool Node 저장
- sandbox를 통한 사용자 코드 격리 실행
- 실행 로그, Agent 로그, MCP 호출 로그, sandbox 로그

## 폴더별 구현 책임

각 구현 폴더는 자체 상세 문서를 가진다.

| 폴더 | 상세 문서 |
|---|---|
| `frontend` | `frontend/docs/spec.md`, `frontend/docs/plan.md` |
| `backend/gateway` | `backend/gateway/docs/spec.md`, `backend/gateway/docs/plan.md` |
| `backend/workflow_engine` | `backend/workflow_engine/docs/spec.md`, `backend/workflow_engine/docs/plan.md` |
| `backend/agent_service` | `backend/agent_service/docs/spec.md`, `backend/agent_service/docs/plan.md` |
| `backend/mcp_server` | `backend/mcp_server/docs/spec.md`, `backend/mcp_server/docs/plan.md` |
| `backend/log_system` | `backend/log_system/docs/spec.md`, `backend/log_system/docs/plan.md` |
| `backend/shared` | `backend/shared/docs/spec.md`, `backend/shared/docs/plan.md` |
| `sandbox` | `sandbox/docs/spec.md`, `sandbox/docs/plan.md` |
| `db` | `db/docs/spec.md`, `db/docs/plan.md` |
| `docker` | `docker/docs/spec.md`, `docker/docs/plan.md` |

### `frontend`

구현할 것:

- 로그인 화면
- workspace 기본 화면
- React Flow workflow editor
- node palette
- Agent prompt panel
- Agent가 만든 Graph Patch preview
- workflow 저장/실행 UI
- MCP connection 설정 UI
- 실행 로그 조회 UI

기술:

- Next.js 16
- React 19
- TypeScript
- React Flow
- Tailwind CSS
- Zustand
- Vitest, Testing Library

### `backend/gateway`

구현할 것:

- HTTP API 서버
- auth API
- user/tenant/permission 검사
- workflow CRUD API
- workflow run 요청 API
- Agent 요청 API proxy
- MCP connection 관리 API
- frontend에 줄 response schema 정리

기술:

- Python 3.13
- FastAPI
- Pydantic v2
- SQLAlchemy 2
- JWT/OAuth
- pwdlib[argon2]
- pytest

### `backend/workflow_engine`

구현할 것:

- 저장된 workflow 실행
- node 실행 순서 계산
- internal node 실행
- MCP Tool Node 실행 요청
- Code Node sandbox 실행 요청
- workflow run 상태 관리
- node output 전달
- retry, timeout, failure 처리

기술:

- Python 3.13
- Celery 5
- Redis 7.4
- Pydantic v2
- SQLAlchemy 2
- httpx

### `backend/agent_service`

구현할 것:

- 자연어 요청 분석
- 내부 node catalog 조회
- 외부 MCP tool catalog 조회
- Graph Patch 생성
- 위험한 tool/node 표시
- 저장 전 preview용 응답 생성
- workflow 직접 저장 금지

기술:

- Python 3.13
- LangGraph
- LiteLLM
- MCP Python SDK
- Pydantic v2
- httpx

### `backend/mcp_server`

구현할 것:

- 외부 MCP server 등록
- MCP tool list 조회
- tool schema snapshot 저장
- MCP Tool Node 실행 경계
- 내부 기능을 MCP endpoint로 노출
- MCP auth, rate limit, audit log 연결

기술:

- Python 3.13
- MCP Python SDK
- FastAPI 또는 MCP Streamable HTTP
- httpx
- Pydantic v2

### `backend/log_system`

구현할 것:

- workflow run log 저장
- node run log 저장
- Agent decision log 저장
- MCP tool call log 저장
- sandbox execution log 저장
- audit log 조회 API에 필요한 query 제공

기술:

- Python 3.13
- SQLAlchemy 2
- PostgreSQL
- structlog 또는 표준 logging
- OpenTelemetry는 MVP 이후 검토

### `backend/shared`

구현할 것:

- 공통 schema
- DB model
- node catalog
- Graph Patch schema
- workflow graph validation
- permission helper
- credential encryption helper
- 에러 코드와 response contract

주의:

- 실행 handler를 넣지 않는다.
- gateway, workflow_engine, agent_service, mcp_server가 함께 쓰는 계약만 둔다.

기술:

- Pydantic v2
- SQLAlchemy 2
- cryptography
- pytest

### `sandbox`

구현할 것:

- 별도 sandbox 서버
- disposable execution container 생성
- 코드 실행 요청 처리
- stdout/stderr/result 반환
- timeout, memory, CPU, pids 제한
- read-only filesystem
- network policy
- non-root execution
- 실행 후 container cleanup

기술:

- Python 3.13
- FastAPI
- Docker SDK 또는 Docker CLI boundary
- Docker isolated container
- pytest

### `db`

구현할 것:

- migration
- seed
- schema 문서
- init SQL

초기 테이블 그룹:

- identity: users, tenants, memberships, sessions, oauth_accounts, api_tokens
- workflow: workflows, workflow_versions, workflow_runs, node_run_logs
- agent: agent_sessions, agent_messages, agent_draft_patches
- mcp: mcp_servers, mcp_tools, mcp_connections, mcp_tool_schema_snapshots
- credential: encrypted_credentials
- knowledge: knowledge_bases, documents, document_chunks, embeddings
- governance: approval_requests, audit_logs, sandbox_runs

기술:

- PostgreSQL 17
- pgvector
- Alembic

### `docker`

구현할 것:

- local Docker Compose
- gateway service
- workflow_engine service
- agent_service service
- mcp_server service
- log_system service
- sandbox service
- frontend service
- postgres service
- redis service
- Dockerfile 보관
- sandbox runtime image 보관

기술:

- Docker Compose
- Dockerfile
- Nginx는 MVP 이후 reverse proxy 단계에서 추가

## 핵심 규칙

- workflow graph에 secret을 저장하지 않는다.
- credential은 `connection_id`로 참조한다.
- credential 원문은 암호화해서 저장한다.
- Agent output은 Graph Patch이며 직접 DB에 저장하지 않는다.
- 사용자가 preview를 확인한 뒤 저장한다.
- MCP tool schema snapshot을 저장해서 breaking change를 감지한다.
- Code Node는 반드시 `sandbox`를 통해 실행한다.
- 사용자 코드는 gateway, workflow_engine, agent_service, mcp_server 안에서 실행하지 않는다.
- log_system은 실행 기록과 감사 기록을 남긴다.
