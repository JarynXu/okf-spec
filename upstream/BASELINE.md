# Upstream Compatibility Baseline

## Normative base

The OKF Library Extension is designed as an additive extension to the upstream Open Knowledge Format specification maintained in `GoogleCloudPlatform/knowledge-catalog`.

Current baseline:

- Open Knowledge Format: v0.2
- Canonical specification: `okf/SPEC.md` in the upstream repository

## Upstream assumptions preserved

The extension preserves these upstream properties:

1. An ordinary OKF bundle remains a hierarchical collection of Markdown concepts with YAML frontmatter.
2. Human and agent readability without mandatory tooling remains a core property.
3. `index.md` remains the progressive-disclosure navigation mechanism for materialized bundles.
4. Git repositories, archives, and repository subdirectories remain valid distribution forms.
5. Existing OKF bundles require no modification to remain valid OKF Core bundles.

## Intentional extension boundary

Upstream OKF deliberately leaves serving, discovery, runtime mounting, and mandatory tooling outside the core format. The Library Extension standardizes optional contracts in this space without changing the meaning of existing OKF documents.

The extension covers:

- Library identity and manifest metadata.
- Runtime registration and mount/unmount semantics.
- A hierarchical virtual knowledge namespace.
- Catalog/navigation contracts.
- Content, query, and source provider contracts.
- Lifecycle and capability declarations.
- Support for materialized and virtual knowledge nodes.

## Relationship to upstream registry proposals

Upstream community proposals have explored bundle-local registries, mount paths, direct Git/archive sources, and catalog adapters. This extension treats those proposals as prior art and aims to remain alignable with them, while using a more general provider-oriented abstraction so remote, distributed, dynamic, and agent-backed libraries are not forced into a filesystem-only model.

## Compatibility rule

An implementation conforming to the Library Extension MUST NOT require an upstream-conformant OKF Core bundle to adopt Library-specific metadata merely to remain consumable as a Core bundle.
