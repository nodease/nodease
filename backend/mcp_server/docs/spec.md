# MCP Server Spec

## 역할

`backend/mcp_server`는 외부 MCP server와 연결하고, Nodease 기능 일부를 MCP endpoint로 노출한다.

## 구현할 것

- 외부 MCP server 등록
- MCP tool list 조회
- tool schema snapshot 저장
- MCP Tool Node 실행 경계
- connection_id 기반 credential 참조
- 내부 MCP endpoint
- MCP auth, rate limit, audit log 연결

## 기술

- Python 3.13
- MCP Python SDK
- Streamable HTTP
- FastAPI
- httpx
- Pydantic v2
- pytest

## 연결 대상

- `backend/shared`: MCP schema, credential reference
- `backend/workflow_engine`: MCP Tool Node 실행 요청
- `backend/agent_service`: tool catalog 제공
- `backend/log_system`: MCP call log
- `db`: MCP server/tool/schema snapshot 저장

## 하지 않을 것

- credential 원문을 workflow graph에 넣지 않는다.
- 인증 없는 MCP 요청을 허용하지 않는다.
- MVP에서 MCP로 workflow 생성/수정 기능을 열지 않는다.
