# OKF Library Extension

Status: draft

The OKF Library Extension enriches Open Knowledge Format with a portable model for independently distributable, mountable, navigable, queryable, and maintainable knowledge units.

It is additive to OKF Core. An ordinary OKF bundle remains valid without Library metadata.

## Core abstractions

A Library combines four logical planes:

1. **Content plane** — knowledge nodes and their content.
2. **Navigation plane** — semantic catalog, topics, aliases, and routing hints.
3. **Query plane** — pluggable retrieval capabilities and a portable result envelope.
4. **Lifecycle plane** — install, mount, refresh, validate, unmount, and uninstall semantics.

The runtime-facing extension points are capability-oriented Providers. Implementations may use a local directory, Git, object storage, HTTP, databases, generated content, or an agent without changing the Library-facing contract.

## Documents

- `SPEC.md` — normative overview and compatibility rules.
- `manifest.md` — portable Library declaration.
- `namespace.md` — virtual knowledge namespace and nodes.
- `provider.md` — provider capability contracts.
- `catalog.md` — semantic navigation contract.
- `query.md` — retrieval model and escalation.
- `query-result.md` — portable query result envelope.
- `lifecycle.md` — runtime lifecycle semantics.
- `security.md` — trust and capability boundaries.

## Reference implementation strategy

The first reference implementation MUST validate the model against three materially different adapters:

- local directory,
- Git repository,
- purely virtual/in-memory provider with no physical knowledge files.

A design that only works for physical files is not considered a valid implementation of this extension.
