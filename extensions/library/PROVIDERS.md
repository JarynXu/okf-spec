# Provider Contracts

Status: Draft

## Purpose

Provider contracts isolate stable Library capabilities from infrastructure-specific implementations. Runtime code depends on these contracts; local filesystems, Git, object storage, remote services, and agent-backed systems are adapters.

## SourceProvider

Resolves a Library reference into a usable Library instance or installation descriptor.

Conceptual operations:

- `resolve(reference)`
- `install(reference, options)`
- `refresh(instance)`
- `revision(instance)`

A source provider MAY materialize content locally, MAY maintain only metadata/cache state, or MAY return a remote/virtual instance.

## CatalogProvider

Returns a semantic, progressively navigable description of the Library.

Conceptual operations:

- `root()`
- `children(node)`
- `describe(node)`
- `resolve_topic(topic)`

Catalog output SHOULD describe domain meaning rather than merely mirror storage paths.

## ContentProvider

Provides hierarchical knowledge nodes independent of physical storage.

Conceptual operations:

- `list(path)`
- `stat(path)`
- `read(path)`
- `resolve(uri)`

A content node MUST NOT be assumed to be a physical file.

## QueryProvider

Executes retrieval strategies declared by a Library.

Conceptual operations:

- `capabilities()`
- `query(request)`

A query request SHOULD be able to express preferred strategy, scope, filters, and result limits without exposing implementation-specific backend details.

A query result SHOULD preserve provenance sufficient for a consumer to inspect the evidence behind retrieved knowledge.

## Composition

Providers are capability roles, not mutually exclusive implementation classes.

One Library may use:

- Git for source/version metadata;
- an object store for content;
- a generated catalog;
- a remote semantic search service;
- an agentic query provider for complex retrieval.

To consumers, the composition remains one Library.

## Architectural rule

Core runtime logic MUST dispatch through provider contracts and MUST NOT branch on concrete infrastructure names such as `local`, `git`, or `s3` except inside adapter selection/configuration code.
