# OKF Specifications

This repository defines compatible extensions to the upstream Open Knowledge Format (OKF) specification.

It does **not** redefine OKF Core. The upstream OKF specification remains the normative base. Extensions in this repository add optional capabilities that intentionally sit outside the current OKF Core scope, such as runtime-manageable libraries, virtual knowledge namespaces, providers, catalogs, query contracts, and lifecycle semantics.

## Status

Early design work. No compatibility guarantee is provided until an extension reaches a stable version.

## Structure

- `upstream/` — compatibility baseline and upstream design notes.
- `extensions/library/` — the OKF Library Extension specification.

## Design principles

1. Preserve compatibility with upstream OKF bundles.
2. Keep OKF knowledge human- and agent-readable.
3. Add machine-readable structure only where deterministic runtime behavior requires it.
4. Separate stable domain contracts from storage and transport implementations.
5. Support local, Git-backed, remote, distributed, and fully virtual knowledge providers through common abstractions.
6. Make catalog/navigation and query behavior explicit so specialized libraries can teach a runtime how their knowledge should be discovered and retrieved.
