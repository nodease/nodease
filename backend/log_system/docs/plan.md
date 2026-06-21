# Log System Plan

## M1. Log Schema

- workflow run log schema를 만든다.
- node run log schema를 만든다.
- audit log schema를 만든다.

검증:

- run_id 기준으로 로그를 조회할 수 있어야 한다.

## M2. Service Boundaries

- workflow_engine 기록 경계를 만든다.
- agent_service 기록 경계를 만든다.
- mcp_server 기록 경계를 만든다.
- sandbox 기록 경계를 만든다.

검증:

- 각 서비스가 표준 log contract를 사용해야 한다.

## M3. Redaction

- secret redaction 규칙을 만든다.
- credential, token, key 패턴을 필터링한다.

검증:

- log에 secret이 남지 않아야 한다.

## M4. Query

- run log 조회 query를 만든다.
- node log 조회 query를 만든다.
- audit log 조회 query를 만든다.

검증:

- tenant별 접근 제한이 적용되어야 한다.
