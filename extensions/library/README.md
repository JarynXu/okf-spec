# OKF Library Extension

Status: v0.2 draft, reference-implementation validated

The OKF Library Extension enriches Open Knowledge Format with independently distributable, mountable, semantically navigable, searchable, and maintainable knowledge units. It is additive to OKF Core: ordinary OKF bundles remain valid without Library metadata.

## Compatibility principle

A mounted Library extends the active OKF knowledge space; it does not introduce a second user-facing knowledge API. Existing OKF consumption operations remain the normal interface before and after Libraries are installed. In particular, `search` remains the canonical user-facing retrieval operation. A runtime may use Library catalogs, routing hints, and provider capabilities internally to choose optimized retrieval strategies.

Library-specific commands or APIs should therefore be reserved primarily for Library management and explicit advanced scoping, such as install, update, mount, unmount, remove, list, or an optional `--library` restriction on an existing knowledge operation.

## Core model

A Library combines four logical planes:

1. **Content** — logical knowledge nodes; physical files are only one implementation.
2. **Navigation** — Library-owned semantic catalog, topics, aliases, vocabulary, and routing hints.
3. **Retrieval** — pluggable exact/lexical/semantic/graph/agentic provider strategies with evidence/provenance, normally reached through existing OKF search operations.
4. **Lifecycle** — install/register, mount, refresh/update, validate, unmount, and uninstall.

Runtime code depends on capability contracts. Local directories, Git, object storage, HTTP, databases, generated nodes, filesystem adapters, and agents are infrastructure adapters rather than branches in the domain model.

## Materialized package profile

A local or Git-materialized Library may declare itself with the canonical `okf-library.yaml` manifest. Schema version `"1"` defines identity, version, curated semantic catalog entries, non-executable retrieval guidance, and optional provider deployment declarations. See `MANIFEST.md` and `PROVIDER-DEPLOYMENT.md`.

## Main documents

- `SPEC.md` — normative overview and compatibility rules.
- `MANIFEST.md` — `okf-library.yaml` v1 package profile.
- `NAMESPACE.md` — virtual namespace and logical nodes.
- `PROVIDERS.md` — capability/provider and composition contracts.
- `PROVIDER-DEPLOYMENT.md` — optional manifest binding of concrete deployment adapters.
- `PROCESS-PROVIDER.md` — language-neutral JSON/stdin/stdout process provider protocol.
- `REMOTE-PROTOCOL.md` — HTTP transport for the same provider semantic envelope.
- `FILESYSTEM.md` — read-only virtual namespace projection across native filesystem technologies.
- `CATALOG-QUERY.md` — semantic catalog and provider retrieval model.
- `query-result.md` — evidence-bearing provider result envelope.
- `LIFECYCLE.md` — Runtime lifecycle semantics.
- `registry.md` / `mount-table.md` — dynamic registry, routes, and global catalog.
- `source.md` — acquisition/source boundary.
- `maintenance.md` — consumption versus knowledge maintenance.
- `security.md` — trust and capability boundaries.
- `mcp-and-filesystem-adapters.md` — adapter guidance for MCP and virtual filesystem views.
- `conformance.md` / `test-matrix.md` — conformance and reference validation.

Concrete domain Libraries and their application-specific profiles belong in their own repositories and MUST NOT become dependencies of the generic OKF specification, SDK, CLI, MCP, or skills.

## Reference implementation validation

The Rust reference runtime validates materially different cases through one abstraction:

- local OKF bundle;
- Git source/materialization;
- purely virtual/in-memory provider with no physical knowledge files;
- process-backed dynamic provider;
- HTTP remote provider;
- S3-compatible content provider;
- SQLite content/catalog/query provider;
- vector semantic query provider;
- cross-platform virtual filesystem projection.

These are adapter implementations over the same capability model. They do not change Library identity or create parallel user-facing knowledge APIs.
