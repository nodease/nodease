# Backend

backend skeleton for the Nodease MVP.

Planned areas:

- `gateway`: HTTP API server, auth boundary, tenant permission checks, and frontend-facing contracts.
- `workflow_engine`: background workflow execution and node run orchestration.
- `agent_service`: natural-language workflow draft generation.
- `mcp_server`: external MCP discovery, MCP Tool Node boundary, and Nodease MCP endpoint.
- `log_system`: workflow, node, Agent, MCP, sandbox, and audit logs.
- `shared`: schemas, DB models, node catalog, graph validation, permissions, and credential helpers.
- `tests`: backend-level tests.

This folder is a skeleton only. Do not add runtime code until the matching milestone in `docs/plan.md`.
