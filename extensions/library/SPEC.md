# OKF Library Extension

Status: Draft

## 1. Purpose

The OKF Library Extension defines a runtime-manageable unit of knowledge that preserves OKF's human- and agent-readable knowledge model while adding machine-readable contracts for discovery, loading, navigation, retrieval, and lifecycle management.

A Library is not a replacement for an OKF bundle. It is an extended OKF knowledge unit whose structure can be consumed both semantically by agents and deterministically by software.

## 2. User-facing compatibility

A mounted Library MUST extend the active OKF knowledge space without requiring consumers to switch to a Library-specific knowledge-consumption API.

Existing OKF consumption operations SHOULD preserve their user-facing meaning when Libraries are present. In particular, a runtime exposing a `search` operation SHOULD search the current OKF knowledge space, including mounted Libraries, and MAY use Library-owned catalogs, routing hints, and provider capabilities to select an optimized retrieval path.

A runtime MAY allow an existing consumption operation to be explicitly scoped to one Library for advanced control or diagnostics. Such scoping MUST be optional for normal use.

Library-specific command groups or APIs SHOULD focus on management concerns such as install/register, update/refresh, mount, unmount, remove/uninstall, and registry inspection. A generic OKF implementation MUST NOT grow application-specific commands merely because a particular Library is installed.

## 3. Core model

A conforming Library exposes four logical planes:

1. **Content Plane** — the knowledge itself.
2. **Navigation Plane** — how the knowledge is organized and progressively discovered.
3. **Retrieval Plane** — how a runtime may retrieve knowledge, including specialized or semantic strategies behind the normal OKF consumption interface.
4. **Lifecycle Plane** — how the Library is identified, loaded, mounted, refreshed, disabled, unmounted, and updated.

The planes are logical contracts. They MAY be implemented by static files, generated views, remote services, or other providers.

## 4. Library

A Library MUST have a stable identity and MUST expose a manifest.

A Library MAY contain a materialized OKF bundle, MAY expose a virtual hierarchy, or MAY combine both.

A Library SHOULD expose:

- a catalog suitable for progressive disclosure;
- content nodes addressable through a stable namespace;
- declared retrieval capabilities;
- lifecycle metadata sufficient for a runtime to manage it deterministically.

## 5. Runtime independence

This specification defines contracts, not one required runtime implementation.

A conforming runtime MAY expose Libraries through an SDK, CLI, MCP server, HTTP service, FUSE-like filesystem, Windows virtual filesystem, or another adapter.

All such adapters SHOULD preserve the same logical Library namespace and capabilities.

## 6. Provider model

Library behavior is expressed through capability-oriented provider contracts rather than storage-type conditionals.

The initial provider roles are:

- `SourceProvider` — resolves or acquires a Library.
- `CatalogProvider` — exposes its semantic navigation structure.
- `ContentProvider` — lists, describes, and reads knowledge nodes.
- `QueryProvider` — executes declared provider-level retrieval strategies behind the runtime's normal search interface.

A single implementation MAY satisfy multiple provider roles.

Provider implementations MAY include local directories, Git repositories, object stores, HTTP services, databases, generated content, or agent-backed retrieval systems.

## 7. Virtual knowledge namespace

A runtime MUST be able to project mounted Libraries into a hierarchical logical namespace.

The namespace MUST NOT require every node to correspond to a physical filesystem object.

A node MAY be:

- materialized content;
- generated content;
- a remote resource proxy;
- a semantic navigation node;
- a runtime status or metadata node.

This allows a Library to appear file-like to consumers while its content is produced dynamically by software.

## 8. Catalog responsibility

Each Library is responsible for describing how its own specialized knowledge should be navigated and retrieved.

A runtime MUST NOT be required to understand the domain semantics of every Library it hosts.

The Library catalog SHOULD therefore expose more than a raw file listing. It SHOULD provide semantic sections, descriptions, topics, aliases, relationships, useful entry points, domain vocabulary, and routing hints sufficient to guide progressive retrieval.

A runtime MAY aggregate mounted Library catalogs into a global catalog and SHOULD use that metadata to avoid unnecessary broad retrieval when a relevant Library or topic can be selected deterministically.

## 9. Retrieval responsibility

A Library MAY declare one or more provider-level retrieval capabilities.

Examples include:

- exact lookup;
- structured filtering;
- lexical search;
- semantic retrieval;
- graph retrieval;
- remote retrieval;
- agentic retrieval.

A runtime SHOULD route a user-facing search through Library-supported strategies rather than assuming one global retrieval implementation is suitable for all knowledge domains. The internal provider operation MAY be named `query`; this does not imply a separate user-facing `query` command.

Agentic retrieval is an optional provider capability, not a requirement for basic Library conformance.

## 10. Lifecycle

A runtime MAY distinguish acquisition from activation:

- **install** acquires or registers a Library source;
- **mount** makes a Library visible in the active knowledge namespace;
- **unmount** removes it from the active namespace without necessarily deleting acquired content;
- **uninstall** removes the installed Library instance or cache.

Additional lifecycle operations such as refresh, update, enable, disable, validate, and invalidate are defined by the lifecycle contract.

## 11. Initial source expectations

The first reference implementation is expected to support:

1. local directory sources;
2. Git repository sources;
3. a fully virtual provider with no required physical knowledge files.

The virtual reference implementation is required as an architectural test: a conforming core design MUST NOT assume that every Library can be materialized as local files.

## 12. Relationship to OKF Core

Existing OKF Core bundles remain valid without Library metadata.

A materialized Library SHOULD preserve ordinary OKF readability wherever its knowledge is stored as Markdown concepts.

Library metadata MUST NOT redefine the semantics of OKF Core frontmatter fields.

Generic OKF repositories MUST remain domain-neutral. Concrete Libraries, application profiles, repository-specific freshness models, and other domain behavior belong outside the generic specification and reference tooling unless the behavior has first been generalized into a domain-independent contract.

## 13. Open design areas

The following are intentionally not frozen in this initial draft:

- provider loading ABI;
- dependency semantics;
- capability negotiation details;
- security and permission model;
- cache consistency model.

These should be specified only after they can be expressed without coupling the generic OKF model to a concrete Library application.
