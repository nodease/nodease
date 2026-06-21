# Log System Spec

## 역할

`backend/log_system`은 workflow, node, Agent, MCP, sandbox, audit log를 저장하고 조회한다. 

## 구현할 것

- workflow run log
- node run log
- Agent decision log
- MCP tool call log
- sandbox execution log
- approval decision log
- audit log query
- secret redaction policy

## 기술

- Python 3.13
- SQLAlchemy 2
- PostgreSQL
- structlog 또는 표준 logging
- pytest

## 연결 대상

- `backend/gateway`: 로그 조회 API
- `backend/workflow_engine`: run/node log 기록
- `backend/agent_service`: decision log 기록
- `backend/mcp_server`: MCP call log 기록
- `sandbox`: execution log metadata
- `db`: 로그 저장

## 하지 않을 것

- credential 원문을 저장하지 않는다.
- LLM prompt 전체를 무조건 저장하지 않는다.
- 로그 조회에서 tenant 경계를 넘기지 않는다.
