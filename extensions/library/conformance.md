# Conformance

An implementation conforms to the OKF Library Extension when it preserves the following observable properties.

## Library conformance

A conforming Library:

- has a stable identity;
- exposes a hierarchical virtual namespace;
- exposes or can produce a semantic catalog;
- declares supported capabilities rather than requiring callers to infer them from storage type;
- preserves provenance for query evidence;
- can be mounted and unmounted without changing the meaning of unrelated Libraries.

## Runtime conformance

A conforming runtime:

- discovers Libraries through explicit registration or configured sources;
- routes operations by Library identity and capability;
- aggregates Library catalogs without erasing Library boundaries;
- treats physical files as one adapter rather than as the abstract model;
- distinguishes mount state from installation/materialization state;
- reports unsupported capabilities deterministically.

## Provider conformance

A provider MUST implement only the capabilities it declares. A runtime MUST NOT emulate an undeclared mutating capability by bypassing the provider abstraction and directly changing provider storage.

## Reference profiles

The initial reference implementation defines three profiles:

- `local`: physical local directory;
- `git`: Git source materialized to a local working/cache directory;
- `virtual`: generated in-memory namespace with no required physical files.

Passing all three profiles is the minimum architecture test for the first SDK implementation.
