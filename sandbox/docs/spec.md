# Sandbox Spec

## 역할

`sandbox`는 사용자 코드를 격리된 disposable container에서 실행하는 별도 서비스다.

## 구현할 것

- sandbox HTTP server
- execution request validation
- disposable Docker container 생성
- stdout/stderr/result 수집
- timeout 제한
- CPU, memory, pids 제한
- read-only filesystem
- network policy
- non-root execution
- cleanup
- audit metadata 반환

## 기술

- Python 3.13
- FastAPI
- Docker SDK 또는 Docker CLI boundary
- Docker isolated container
- pytest

## 연결 대상

- `backend/workflow_engine`: Code Node 실행 요청
- `backend/log_system`: sandbox execution log metadata
- `docker`: sandbox runtime image와 Compose 설정

## 하지 않을 것

- sandbox server 프로세스 안에서 사용자 코드를 직접 실행하지 않는다.
- privileged container를 쓰지 않는다.
- Docker socket을 실행 컨테이너에 노출하지 않는다.
