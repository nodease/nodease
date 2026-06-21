# Agent Service Spec

## 역할

`backend/agent_service`는 자연어 요청을 저장 가능한 workflow 초안으로 바꾼다.

## 구현할 것

- Agent request API 또는 worker boundary
- internal node catalog 조회
- 외부 MCP tool catalog 조회
- LangGraph planning flow
- LiteLLM model call
- Graph Patch 생성
- 위험한 node/tool 표시
- preview 전용 응답

## 기술

- Python 3.13
- LangGraph
- LiteLLM
- MCP Python SDK
- Pydantic v2
- httpx
- pytest

## 연결 대상

- `backend/shared`: node catalog, Graph Patch schema
- `backend/mcp_server`: 외부 MCP tool catalog 조회
- `backend/log_system`: Agent decision log
- `backend/gateway`: frontend 요청 입구

## 하지 않을 것

- workflow를 직접 저장하지 않는다.
- credential 원문을 다루지 않는다.
- 사용자 승인 없이 위험한 tool 실행을 예약하지 않는다.
