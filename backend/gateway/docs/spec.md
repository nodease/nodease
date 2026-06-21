# Gateway Spec

## 역할

`backend/gateway`는 frontend와 외부 HTTP 요청이 들어오는 백엔드 입구다.

## 구현할 것

- FastAPI HTTP server
- auth API
- user/tenant/permission 검사
- workflow CRUD API
- workflow run 요청 API
- Agent draft 요청 proxy
- MCP connection 관리 API
- log 조회 API proxy
- 공통 request/response contract

## 기술

- Python 3.13
- FastAPI
- Pydantic v2
- SQLAlchemy 2
- JWT/OAuth
- pwdlib[argon2]
- httpx
- pytest

## 연결 대상

- `backend/shared`: schema, model, validation, permission
- `backend/workflow_engine`: workflow 실행 enqueue
- `backend/agent_service`: Agent draft 생성 요청
- `backend/mcp_server`: MCP connection과 tool 조회
- `backend/log_system`: 로그 조회
- `db`: PostgreSQL

## 하지 않을 것

- workflow node 실행을 직접 하지 않는다.
- 사용자 코드를 실행하지 않는다.
- LLM planning을 직접 하지 않는다.
