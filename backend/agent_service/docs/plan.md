# Agent Service Plan

## M1. Agent Contract

- Agent request/response schema를 만든다.
- Graph Patch response를 shared schema에 맞춘다.

검증:

- 응답은 항상 preview 가능한 Graph Patch여야 한다.

## M2. Catalog Loading

- internal node catalog를 읽는다.
- MCP tool catalog를 mcp_server에서 읽는다.

검증:

- Agent prompt에 사용 가능한 node/tool 설명이 들어가야 한다.

## M3. Planning Flow

- LangGraph planning flow를 만든다.
- LiteLLM model 호출 경계를 만든다.
- tool 위험도를 표시한다.

검증:

- 저장 가능한 workflow draft가 생성되어야 한다.

## M4. Preview Safety

- Agent 결과를 DB에 직접 저장하지 않는다.
- gateway/frontend가 preview 후 저장하게 한다.

검증:

- Agent 단독 호출로 workflow가 생성되면 안 된다.

## M5. Logging

- Agent decision log를 log_system에 남긴다.

검증:

- 어떤 node/tool을 선택했는지 추적 가능해야 한다.
