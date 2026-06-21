# Docker Plan

## M1. Base Compose

- postgres service를 만든다.
- redis service를 만든다.
- 공통 network를 만든다.

검증:

- `docker compose config`가 통과해야 한다.

## M2. App Services

- frontend service를 만든다.
- gateway service를 만든다.
- workflow_engine service를 만든다.
- agent_service service를 만든다.
- mcp_server service를 만든다.
- log_system service를 만든다.

검증:

- 서비스들이 Compose service name으로 통신해야 한다.

## M3. Sandbox Service

- sandbox service를 만든다.
- sandbox runtime image를 분리한다.
- resource limit과 network policy를 설정한다.

검증:

- sandbox는 다른 서비스보다 제한된 권한으로 떠야 한다.

## M4. Environment

- `.env.example`을 정리한다.
- secret은 placeholder만 둔다.

검증:

- 실제 secret이 repository에 없어야 한다.
