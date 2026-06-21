# Workflow Engine Spec

## 역할

`backend/workflow_engine`은 저장된 workflow를 백그라운드에서 실행한다. 

## 구현할 것

- Celery worker
- workflow graph loading
- node 실행 순서 계산
- internal node 실행
- MCP Tool Node 실행 요청
- Code Node sandbox 실행 요청
- workflow_runs 상태 관리
- node_run_logs 기록
- retry, timeout, failure 처리

## 기술

- Python 3.13
- Celery 5
- Redis 7.4
- Pydantic v2
- SQLAlchemy 2
- httpx
- pytest

## 연결 대상

- `backend/shared`: graph schema, node catalog, validation
- `backend/mcp_server`: MCP Tool Node 실행 경계
- `sandbox`: Code Node 실행
- `backend/log_system`: 실행 로그 기록
- `db`: workflow와 run 상태 저장

## 하지 않을 것

- HTTP frontend API를 직접 제공하지 않는다.
- Agent draft를 생성하지 않는다.
- 사용자 코드를 프로세스 내부에서 실행하지 않는다.
