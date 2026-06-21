# Sandbox

Separate sandbox service skeleton for isolated user-code execution.

Planned areas:

- `server`: sandbox service request boundary.
- `runtimes`: runtime image and language execution assets.
- `policies`: network, filesystem, timeout, and resource-limit policies.
- `tests`: sandbox service tests.

The sandbox service should manage disposable execution containers. It should not execute user code inside the service process.
