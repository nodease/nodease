# Gateway Plan

## M1. Server Boundary

- FastAPI app을 만든다.
- health endpoint를 만든다.
- 공통 에러 응답 형식을 정한다.

검증:

- health endpoint가 응답해야 한다.

## M2. Auth API

- signup/login/session API를 만든다.
- JWT session을 연결한다.
- tenant context를 resolve한다.

검증:

- 인증 없는 요청은 보호 API에 접근할 수 없어야 한다.

## M3. Workflow API

- workflow CRUD API를 만든다.
- graph validation을 shared에 위임한다.
- workflow version 저장을 연결한다.

검증:

- invalid graph는 저장되지 않아야 한다.

## M4. Execution API

- workflow run 요청 API를 만든다.
- workflow_engine enqueue 경계를 만든다.

검증:

- gateway가 실행 로직 없이 run 요청만 전달해야 한다.

## M5. Integration API

- Agent draft 요청 API를 만든다.
- MCP connection API를 만든다.
- log 조회 API를 만든다.

검증:

- 각 요청은 담당 서비스로 위임되어야 한다.
