# Adapter Guidance

The Library Extension defines logical capabilities, not presentation transports.

## Filesystem adapter

A filesystem adapter may expose the virtual knowledge namespace as files and directories. Linux FUSE, Windows virtual filesystem technologies, or process-generated pseudo-files are valid implementations. Physical files are not required. Reading a virtual node invokes the owning provider.

## MCP adapter

An MCP adapter may expose Library list/catalog/read/query operations as tools or resources. It should preserve canonical knowledge URIs and provenance so callers can move between CLI, SDK, MCP, HTTP, and filesystem views without changing knowledge identity.

## Rule

Adapters MUST NOT become the normative data model. Runtime and Library domain logic remain usable without any particular adapter.
