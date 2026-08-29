# Serialization

The v0.1 materialized Library package profile now freezes the canonical package manifest as `okf-library.yaml` with `schema_version: "1"`.

The normative fields and semantics are defined in `MANIFEST.md`. Runtime registry/cache serialization remains an implementation detail and is not a portable Library format.

Virtual and remote Libraries may provide the same manifest model through provider registration rather than a physical YAML file. This preserves the semantic model while allowing distributed or program-backed Libraries.
