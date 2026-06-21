# Sandbox Plan

## M1. Server Boundary

- FastAPI sandbox server를 만든다.
- execution request/response schema를 만든다.

검증:

- 잘못된 실행 요청은 거절되어야 한다.

## M2. Container Runner

- disposable Docker container를 생성한다.
- 실행 후 container를 정리한다.
- stdout/stderr/result를 반환한다.

검증:

- 실행 후 남는 container가 없어야 한다.

## M3. Isolation Policy

- non-root 실행을 적용한다.
- read-only filesystem을 적용한다.
- CPU, memory, pids 제한을 적용한다.
- timeout을 적용한다.

검증:

- 제한을 넘는 코드는 실패해야 한다.

## M4. Network Policy

- 기본 network policy를 정한다.
- 허용된 outbound만 열 수 있게 한다.

검증:

- 차단된 네트워크 접근은 실패해야 한다.

## M5. Audit

- execution metadata를 반환한다.
- log_system에 남길 필드를 정의한다.

검증:

- 누가 어떤 코드 실행을 요청했는지 추적 가능해야 한다.
