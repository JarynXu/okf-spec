# Error Model

Library operations should fail with machine-distinguishable categories: unknown-library, not-mounted, unsupported-capability, invalid-uri, node-not-found, source-resolution-failed, provider-failed, validation-failed, and conflict.

Adapters may add transport-specific diagnostics but should preserve the stable category so CLI, MCP, and SDK callers can make deterministic decisions.
