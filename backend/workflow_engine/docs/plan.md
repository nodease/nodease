# Workflow Engine Plan

## M1. Worker Process

- Celery app을 만든다.
- Redis broker/result backend를 연결한다.
- run task entrypoint를 만든다.

검증:

- gateway가 run task를 enqueue할 수 있어야 한다.

## M2. Graph Execution

- workflow graph를 로드한다.
- node 실행 순서를 계산한다.
- node input/output context를 만든다.

검증:

- 이전 node output이 다음 node input으로 전달되어야 한다.

## M3. Node Handlers

- start node handler를 만든다.
- answer node handler를 만든다.
- LLM placeholder node handler를 만든다.
- MCP placeholder node handler를 만든다.

검증:

- 최소 workflow가 성공 상태로 끝나야 한다.

## M4. External Boundaries

- MCP Tool Node는 mcp_server를 통해 실행한다.
- Code Node는 sandbox를 통해 실행한다.

검증:

- 사용자 코드는 workflow_engine 내부에서 실행되지 않아야 한다.

## M5. Run State

- workflow_runs 상태를 기록한다.
- node_run_logs를 기록한다.
- 실패와 timeout을 기록한다.

검증:

- 실패한 node의 에러가 추적 가능해야 한다.
