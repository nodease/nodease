# Docker Spec

## 역할

`docker`는 local runtime, Compose, Dockerfile, sandbox runtime image를 관리한다.

## 구현할 것

- local Docker Compose
- frontend service
- gateway service
- workflow_engine service
- agent_service service
- mcp_server service
- log_system service
- sandbox service
- postgres service
- redis service
- service network
- sandbox network policy
- Dockerfile 보관

## 기술

- Docker Compose
- Dockerfile
- PostgreSQL 17
- Redis 7.4
- sandbox runtime images
- Nginx는 MVP 이후 검토

## 하지 않을 것

- production Kubernetes 구성을 MVP에 넣지 않는다.
- sandbox 실행 컨테이너에 Docker socket을 넘기지 않는다.
- secret을 Compose 파일에 하드코딩하지 않는다.
