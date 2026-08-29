# Library Manifest

Status: Draft v0.1 implementation profile

## Purpose

The Library manifest is the machine-readable declaration that lets a runtime identify a materialized Library and consume its Library-owned semantic navigation/query guidance without inferring domain structure from storage paths.

The canonical v0.1 materialized-package manifest is:

```text
okf-library.yaml
```

It lives at the Library root. Virtual/remote Libraries MAY provide an equivalent manifest model through provider registration instead of a physical file.

## Schema version 1

```yaml
schema_version: "1"
id: mcx
name: Mission Critical Services
version: "2026.1"

catalog:
  - id: xcap
    title: XCAP interfaces
    description: XCAP documents, selectors, AUIDs, and procedures.
    path: interfaces/xcap
    terms: [xcap, auid, document-selector]

query:
  preferred: semantic
  capabilities: [lexical, semantic, agentic]
  hints:
    - Prefer interfaces/xcap for XCAP terminology.
```

### Required fields

- `schema_version`: MUST be `"1"` for this profile.
- `id`: stable Library identifier. It MUST contain only portable identifier characters accepted by the Runtime.
- `name`: human-readable Library name.

### Optional fields

- `version`: Library knowledge/package version.
- `catalog`: semantic navigation entries owned by the Library.
- `query`: retrieval guidance.

Each catalog entry has:

- `id`: stable semantic topic identifier;
- `title`: display title;
- `description`: optional topic scope explanation;
- `path`: logical path inside the Library namespace, resolved as `okf://<library-id>/<path>`;
- `terms`: optional aliases/domain vocabulary used for routing and discovery.

The `query` object may contain:

- `preferred`: preferred retrieval mode such as `lexical`, `semantic`, `graph`, or `agentic`;
- `capabilities`: retrieval modes the Library expects to support when corresponding providers are available;
- `hints`: domain-specific routing/search guidance for query providers.

Query declarations do not execute code and do not grant capabilities. Runtime/provider registration remains responsible for binding concrete query implementations.

## Runtime/source separation

Portable package metadata does not embed local installation paths, Git cache paths, credentials, or secrets. Acquisition metadata such as Local/Git source belongs to Runtime registration state. A Runtime combines package identity/catalog/query guidance with its resolved `LibrarySource` to form an active Library instance.

## Semantic ownership

The manifest MAY carry a curated semantic catalog because that catalog expresses how the Library wants its knowledge navigated. The host MUST prefer a valid Library-owned catalog over inventing domain structure from filenames. When no explicit catalog is present, an adapter MAY derive a fallback catalog from OKF document metadata.

## Compatibility

Ordinary OKF Core bundles without `okf-library.yaml` remain valid OKF bundles. A Runtime MAY mount them through an adapter using explicit Runtime identity; they simply do not provide package-level semantic navigation/query declarations.

## Security

Manifest content is data, not executable instructions. Credentials and secrets MUST NOT be stored in the portable manifest. Provider/runtime configuration supplies authentication and execution authority separately.
