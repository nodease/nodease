# DB Spec

## 역할

`db`는 PostgreSQL schema, migration, seed, init SQL을 관리한다.

## 구현할 것

- Alembic migration
- local seed
- init SQL
- schema design notes
- pgvector extension setup

## 기술

- PostgreSQL 17
- pgvector
- Alembic
- SQLAlchemy 2 model sync

## 초기 테이블 그룹

- identity: users, tenants, memberships, sessions, oauth_accounts, api_tokens
- workflow: workflows, workflow_versions, workflow_runs, node_run_logs
- agent: agent_sessions, agent_messages, agent_draft_patches
- mcp: mcp_servers, mcp_tools, mcp_connections, mcp_tool_schema_snapshots
- credential: encrypted_credentials
- knowledge: knowledge_bases, documents, document_chunks, embeddings
- governance: approval_requests, audit_logs, sandbox_runs

## 하지 않을 것

- application logic을 넣지 않는다.
- credential 원문 seed를 넣지 않는다.
