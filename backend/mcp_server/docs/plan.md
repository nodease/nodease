# MCP Server Plan

## M1. Registry

- MCP server 등록 모델을 만든다.
- connection_id 기반 인증 참조를 만든다.

검증:

- secret 원문이 workflow graph에 들어가지 않아야 한다.

## M2. Tool Discovery

- MCP Python SDK로 tool list를 조회한다.
- tool schema snapshot을 저장한다.

검증:

- schema 변경 감지가 가능해야 한다.

## M3. Tool Execution Boundary

- MCP Tool Node 실행 요청을 받는다.
- connection_id로 credential을 resolve한다.
- 결과와 에러를 표준 형태로 반환한다.

검증:

- workflow_engine이 MCP Tool Node를 실행할 수 있어야 한다.

## M4. Nodease MCP Endpoint

- Streamable HTTP MCP endpoint를 만든다.
- list_workflows, run_workflow, get_run_status, search_knowledge를 노출한다.

검증:

- 인증 없는 요청은 거절되어야 한다.

## M5. Audit

- MCP tool call log를 남긴다.
- rate limit과 permission check를 연결한다.

검증:

- 누가 어떤 MCP tool을 호출했는지 추적 가능해야 한다.
