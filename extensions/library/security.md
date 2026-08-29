# Security and Trust Boundaries

OKF Library providers are extension points and may cross process, network, or trust boundaries. The Library Extension therefore treats provider execution and knowledge consumption as separate concerns.

## Requirements

- A runtime MUST identify the Library and provider that produced a result.
- A runtime MUST NOT treat Library content as executable instructions merely because it is mounted.
- Provider-specific credentials MUST remain outside portable Library content and SHOULD be supplied by the runtime or deployment environment.
- A remote or dynamic provider SHOULD expose a stable identity and version/revision when available.
- A runtime MAY restrict capabilities by Library or caller, including `read`, `query`, `refresh`, and maintenance operations.
- A runtime SHOULD support read-only mounts.

## Agent-backed query providers

An agent-backed query provider is a retrieval implementation, not an authority boundary. It MUST obey the same evidence and provenance requirements as other providers. A host SHOULD isolate the tools available to a query agent from tools that can mutate the underlying knowledge source unless maintenance is explicitly requested.

## Non-goals

This extension does not prescribe an authentication protocol, secret manager, sandbox technology, or network transport. Those are adapter and deployment concerns.
