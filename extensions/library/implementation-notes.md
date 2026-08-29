# Reference Implementation Notes

The Rust reference implementation belongs in `okf-sdk` and should expose domain types and traits without depending on CLI, MCP, FUSE, or network transports.

The CLI remains a thin adapter over the SDK. The MCP server should likewise delegate Library operations to the SDK/CLI boundary rather than reimplementing parsing, registry, routing, or query semantics.

The first implementation should favor a small auditable surface over speculative abstraction. New provider traits should be introduced only when they represent a stable capability required by at least one validation profile.
