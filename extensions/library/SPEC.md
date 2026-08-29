# OKF Library Extension

Status: Draft

## 1. Purpose

The OKF Library Extension defines a runtime-manageable unit of knowledge that preserves OKF's human- and agent-readable knowledge model while adding machine-readable contracts for discovery, loading, navigation, querying, and lifecycle management.

A Library is not a replacement for an OKF bundle. It is an extended OKF knowledge unit whose structure can be consumed both semantically by agents and deterministically by software.

## 2. Core model

A conforming Library exposes four logical planes:

1. **Content Plane** — the knowledge itself.
2. **Navigation Plane** — how the knowledge is organized and progressively discovered.
3. **Query Plane** — how consumers may retrieve knowledge, including specialized or semantic retrieval.
4. **Lifecycle Plane** — how the Library is identified, loaded, mounted, refreshed, disabled, unmounted, and updated.

The planes are logical contracts. They MAY be implemented by static files, generated views, remote services, or other providers.

## 3. Library

A Library MUST have a stable identity and MUST expose a manifest.

A Library MAY contain a materialized OKF bundle, MAY expose a virtual hierarchy, or MAY combine both.

A Library SHOULD expose:

- a catalog suitable for progressive disclosure;
- content nodes addressable through a stable namespace;
- declared query capabilities;
- lifecycle metadata sufficient for a runtime to manage it deterministically.

## 4. Runtime independence

This specification defines contracts, not one required runtime implementation.

A conforming runtime MAY expose Libraries through an SDK, CLI, MCP server, HTTP service, FUSE-like filesystem, Windows virtual filesystem, or another adapter.

All such adapters SHOULD preserve the same logical Library namespace and capabilities.

## 5. Provider model

Library behavior is expressed through capability-oriented provider contracts rather than storage-type conditionals.

The initial provider roles are:

- `SourceProvider` — resolves or acquires a Library.
- `CatalogProvider` — exposes its semantic navigation structure.
- `ContentProvider` — lists, describes, and reads knowledge nodes.
- `QueryProvider` — executes declared retrieval strategies.

A single implementation MAY satisfy multiple provider roles.

Provider implementations MAY include local directories, Git repositories, object stores, HTTP services, databases, generated content, or agent-backed retrieval systems.

## 6. Virtual knowledge namespace

A runtime MUST be able to project mounted Libraries into a hierarchical logical namespace.

The namespace MUST NOT require every node to correspond to a physical filesystem object.

A node MAY be:

- materialized content;
- generated content;
- a remote resource proxy;
- a semantic navigation node;
- a runtime status or metadata node.

This allows a Library to appear file-like to consumers while its content is produced dynamically by software.

## 7. Catalog responsibility

Each Library is responsible for describing how its own specialized knowledge should be navigated.

A runtime MUST NOT be required to understand the domain semantics of every Library it hosts.

The Library catalog SHOULD therefore expose more than a raw file listing. It SHOULD provide semantic sections, descriptions, topics, aliases, relationships, and useful entry points sufficient to guide progressive retrieval.

A runtime MAY aggregate mounted Library catalogs into a global catalog.

## 8. Query responsibility

A Library MAY declare one or more query capabilities.

Examples include:

- exact lookup;
- structured filtering;
- lexical search;
- semantic retrieval;
- graph retrieval;
- remote query;
- agentic retrieval.

A runtime SHOULD route a query through a Library-supported strategy rather than assuming one global retrieval implementation is suitable for all knowledge domains.

Agentic retrieval is an optional provider capability, not a requirement for basic Library conformance.

## 9. Lifecycle

A runtime MAY distinguish acquisition from activation:

- **install** acquires or registers a Library source;
- **mount** makes a Library visible in the active knowledge namespace;
- **unmount** removes it from the active namespace without necessarily deleting acquired content;
- **uninstall** removes the installed Library instance or cache.

Additional lifecycle operations such as refresh, update, enable, disable, validate, and invalidate are defined by the lifecycle contract.

## 10. Initial source expectations

The first reference implementation is expected to support:

1. local directory sources;
2. Git repository sources;
3. a fully virtual provider with no required physical knowledge files.

The virtual reference implementation is required as an architectural test: a conforming core design MUST NOT assume that every Library can be materialized as local files.

## 11. Relationship to OKF Core

Existing OKF Core bundles remain valid without Library metadata.

A materialized Library SHOULD preserve ordinary OKF readability wherever its knowledge is stored as Markdown concepts.

Library metadata MUST NOT redefine the semantics of OKF Core frontmatter fields.

## 12. Open design areas

The following are intentionally not frozen in this initial draft:

- exact manifest serialization and filename;
- canonical URI scheme spelling;
- provider loading ABI;
- dependency semantics;
- capability negotiation details;
- query result envelope;
- security and permission model;
- cache consistency model.

These will be specified after validating the domain model against local, Git, and virtual providers.
