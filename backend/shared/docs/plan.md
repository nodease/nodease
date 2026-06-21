# Shared Plan

## M1. Schema Foundation

- workflow graph schema를 만든다.
- Graph Patch schema를 만든다.
- MCP Tool Node schema를 만든다.

검증:

- invalid graph와 unknown node type을 거절해야 한다.

## M2. Node Catalog

- internal node catalog 구조를 만든다.
- node description, input schema, output schema, risk level을 정의한다.

검증:

- Agent가 node 설명을 읽을 수 있어야 한다.

## M3. DB Models

- identity model을 만든다.
- workflow model을 만든다.
- MCP/credential/log model을 만든다.

검증:

- migration과 model이 일치해야 한다.

## M4. Security Helpers

- tenant permission helper를 만든다.
- credential encryption helper를 만든다.

검증:

- secret은 암호화 경계 밖으로 나오지 않아야 한다.

## M5. Contracts

- error code를 정리한다.
- response contract를 정리한다.

검증:

- gateway와 frontend가 같은 contract를 기준으로 통신해야 한다.
