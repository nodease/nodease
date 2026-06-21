# DB Plan

## M1. Migration Setup

- Alembic 환경을 만든다.
- PostgreSQL 연결 설정을 정한다.

검증:

- 빈 migration 흐름이 동작해야 한다.

## M2. Identity Schema

- users, tenants, memberships, sessions를 만든다.

검증:

- tenant별 사용자 권한을 표현할 수 있어야 한다.

## M3. Workflow Schema

- workflows, workflow_versions를 만든다.
- workflow_runs, node_run_logs를 만든다.

검증:

- workflow draft와 실행 이력을 분리해서 저장해야 한다.

## M4. Agent/MCP/Credential Schema

- agent draft 관련 테이블을 만든다.
- MCP registry와 schema snapshot 테이블을 만든다.
- encrypted_credentials 테이블을 만든다.

검증:

- workflow graph는 connection_id만 저장해야 한다.

## M5. Knowledge/Governance Schema

- knowledge base와 embedding 테이블을 만든다.
- approval_requests와 audit_logs를 만든다.

검증:

- 감사 로그와 승인 기록을 조회할 수 있어야 한다.
