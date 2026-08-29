# Library Manifest

Status: Draft

## Purpose

The Library manifest is the machine-readable declaration that allows a runtime to identify a Library and discover the capabilities needed to manage it deterministically.

The manifest describes the Library as a runtime object. It does not replace OKF concept frontmatter and MUST NOT duplicate domain knowledge that belongs in the knowledge corpus.

## Required semantic fields

A stable version of the extension is expected to require at least:

- Library identity;
- Library specification version;
- human-readable name/title;
- provider/capability declarations sufficient to locate catalog and content behavior.

## Candidate optional fields

The following are expected but not yet frozen:

- Library semantic version;
- description;
- source metadata;
- namespace preferences;
- query capabilities and preferred strategy;
- dependencies;
- update/freshness policy;
- permissions/security requirements;
- provider configuration references.

## Separation of concerns

The manifest SHOULD describe capabilities, endpoints, provider references, and lifecycle behavior. It SHOULD NOT be a manually duplicated table of contents when the Library can expose its current catalog dynamically.

Similarly, storage credentials and secrets MUST NOT be embedded directly in a portable Library manifest. Implementations SHOULD reference runtime-managed credential identities or configuration slots.

## Serialization

The canonical manifest filename and serialization format remain open in this draft. YAML is a likely initial representation because it aligns with OKF frontmatter conventions, but the semantic model is normative and should not depend on one parser or programming language.

## Static and virtual Libraries

A materialized local Library may store its manifest alongside its OKF content.

A virtual or remote Library may obtain equivalent manifest data from a provider registration mechanism. A runtime MAY cache such metadata locally.

Both forms MUST be projected into the same logical Library model after resolution.
