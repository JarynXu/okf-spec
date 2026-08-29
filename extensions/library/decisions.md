# Accepted Design Decisions

- Library is an additive OKF extension, not a separate competing standard.
- The runtime's global knowledge catalog is dynamic derived state.
- A Library must contribute semantic navigation, not only a storage location.
- Query is polymorphic and may escalate to semantic or agent-backed retrieval.
- Provider capabilities are abstract; Local, Git, S3, HTTP, databases, and agents are adapters/implementations.
- Virtual knowledge nodes are first-class and need not correspond to physical files.
- Source acquisition is separate from runtime content/query providers.
- Consumption and maintenance are separate capability surfaces.
- Project Context is a Library profile built on these primitives.
