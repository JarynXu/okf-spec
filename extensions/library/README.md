# OKF Library Extension

Status: v0.1 draft, reference-implementation validated

The OKF Library Extension enriches Open Knowledge Format with independently distributable, mountable, semantically navigable, queryable, and maintainable knowledge units. It is additive to OKF Core: ordinary OKF bundles remain valid without Library metadata.

## Core model

A Library combines four logical planes:

1. **Content** — logical knowledge nodes; physical files are only one implementation.
2. **Navigation** — Library-owned semantic catalog, topics, aliases, vocabulary, and routing hints.
3. **Query** — pluggable exact/lexical/semantic/graph/agentic retrieval with evidence/provenance.
4. **Lifecycle** — install/register, mount, refresh/update, validate, unmount, and uninstall.

Runtime code depends on capability contracts. Local directories, Git, object storage, HTTP, databases, generated nodes, filesystem adapters, and agents are infrastructure adapters rather than branches in the domain model.

## Materialized package profile

A local or Git-materialized Library may declare itself with the canonical `okf-library.yaml` manifest. Schema version `"1"` defines identity, version, curated semantic catalog entries, and non-executable query guidance. See `MANIFEST.md`.

## Main documents

- `SPEC.md` — normative overview and compatibility rules.
- `MANIFEST.md` — `okf-library.yaml` v1 package profile.
- `NAMESPACE.md` — virtual namespace and logical nodes.
- `PROVIDERS.md` — capability/provider and composition contracts.
- `CATALOG-QUERY.md` — semantic catalog and retrieval model.
- `query-result.md` — evidence-bearing result envelope.
- `LIFECYCLE.md` — Runtime lifecycle semantics.
- `registry.md` / `mount-table.md` — dynamic registry, routes, and global catalog.
- `source.md` — acquisition/source boundary.
- `maintenance.md` — consumption versus knowledge maintenance.
- `security.md` — trust and capability boundaries.
- `mcp-and-filesystem-adapters.md` — adapter guidance for MCP and virtual filesystem views.
- `project-context-profile.md` — Project Context as a Library profile.
- `conformance.md` / `test-matrix.md` — conformance and reference validation.

## Reference implementation validation

The Rust reference runtime validates three materially different cases through one abstraction:

- local OKF bundle;
- Git source/materialization;
- purely virtual/in-memory provider with no physical knowledge files.

The SDK additionally exposes capability-specific `CatalogProvider`, `ContentProvider`, `QueryProvider`, and `RefreshProvider` roles that can be composed into one Runtime-facing Library provider, plus a pluggable source-resolver contract. This allows future S3/object-storage, HTTP, database, remote, or agent-backed adapters without changing Runtime routing.
