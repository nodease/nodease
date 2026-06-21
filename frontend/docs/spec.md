# Frontend Spec

## 역할

`frontend`는 사용자가 workflow를 만들고 실행 결과를 확인하는 화면이다. 

## 구현할 것

- 로그인/세션 화면
- workspace 기본 화면
- workflow 목록
- React Flow 기반 workflow editor
- node palette
- Agent prompt panel
- Agent Graph Patch preview
- workflow 저장/실행 버튼
- MCP connection 설정 화면
- run log와 node log 조회 화면

## 기술

- Next.js 16
- React 19
- TypeScript
- React Flow
- Tailwind CSS
- Zustand
- Vitest
- Testing Library

## 연결 대상

- `backend/gateway`: 모든 HTTP 요청
- `backend/agent_service`: gateway를 통한 Agent draft 요청
- `backend/log_system`: gateway를 통한 로그 조회

## 하지 않을 것

- workflow 실행 로직을 넣지 않는다.
- Agent planning을 프론트에서 하지 않는다.
- credential 원문을 저장하지 않는다.
