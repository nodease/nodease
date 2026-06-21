# Shared Spec

## 역할

`backend/shared`는 backend 서비스들이 함께 쓰는 계약을 둔다. 

## 구현할 것

- 공통 Pydantic schema
- SQLAlchemy DB model
- workflow graph schema
- Graph Patch schema
- MCP Tool Node schema
- internal node catalog
- graph validation
- permission helper
- credential encryption helper
- error code와 response contract

## 기술

- Python 3.13
- Pydantic v2
- SQLAlchemy 2
- cryptography
- pytest

## 연결 대상

- `backend/gateway`
- `backend/workflow_engine`
- `backend/agent_service`
- `backend/mcp_server`
- `backend/log_system`

## 하지 않을 것

- 실행 handler를 넣지 않는다.
- 외부 HTTP 호출을 넣지 않는다.
- Celery task를 넣지 않는다.
