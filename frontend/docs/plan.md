# Frontend Plan

## M1. App Shell

- Next.js app shell을 만든다.
- 로그인 전/후 레이아웃을 나눈다.
- API client 경계를 만든다.

검증:

- 로그인 전 화면과 로그인 후 shell이 분리되어야 한다.

## M2. Workflow List

- workflow 목록 화면을 만든다.
- 생성, 삭제, 상세 이동 동선을 만든다.

검증:

- gateway API contract로 목록을 불러올 수 있어야 한다.

## M3. Workflow Editor

- React Flow canvas를 만든다.
- node palette와 edge 연결을 만든다.
- graph JSON 저장 요청을 연결한다.

검증:

- workflow를 저장하고 다시 열 수 있어야 한다.

## M4. Agent Preview

- Agent prompt panel을 만든다.
- Graph Patch preview를 만든다.
- 사용자가 accept해야 저장되도록 한다.

검증:

- Agent 응답이 자동 저장되지 않아야 한다.

## M5. Run Logs

- workflow 실행 요청 버튼을 만든다.
- run status와 node log 조회 화면을 만든다.

검증:

- 실패한 node의 에러를 화면에서 확인할 수 있어야 한다.
