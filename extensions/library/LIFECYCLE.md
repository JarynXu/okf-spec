# Library Lifecycle

Status: Draft

## Goal

Library lifecycle semantics separate obtaining knowledge from making it active in a runtime.

## States

A runtime SHOULD be able to distinguish at least:

- `available` — known to the runtime but not acquired;
- `installed` — acquired or registered and ready for activation;
- `mounted` — present in the active knowledge namespace;
- `disabled` — retained but excluded from normal routing;
- `stale` — requires refresh or validation before trusted use;
- `error` — cannot currently satisfy its declared contract.

Exact state-machine details remain implementation-defined in this draft.

## Operations

### install

Acquire or register a Library source. Installation MAY clone content, populate a cache, save connection metadata, or register a virtual/remote provider without downloading the full knowledge corpus.

### mount

Activate a Library in the runtime namespace and global catalog. Mounting SHOULD validate required manifest and provider capabilities.

### unmount

Remove a Library from active routing and namespace projection without necessarily deleting installed data or cache state.

### uninstall

Remove the installed instance, registration, or managed cache. External source data MUST NOT be deleted unless the provider explicitly owns it and the operation was requested accordingly.

### refresh

Ask the source/provider to determine whether metadata, catalog, indexes, or content have changed and update runtime state as appropriate.

### validate

Verify that the Library satisfies declared contracts and any required OKF Core conformance rules for its materialized content.

## Version and revision

Library semantic version and source revision are distinct concepts.

Examples:

- a Git-backed Library may report Library version `1.2.0` and Git revision `<commit>`;
- a local live Library may have no immutable source revision;
- a remote Library may expose an opaque revision token or ETag.

The runtime SHOULD preserve provider-specific revision evidence without forcing all sources into Git semantics.

## Determinism

Lifecycle transitions that affect active routing SHOULD be explicit and machine-observable. A runtime SHOULD NOT require an LLM to infer whether a Library is mounted, stale, or available.
