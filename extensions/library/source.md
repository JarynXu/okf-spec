# Library Sources

A Library Source describes how a runtime can obtain or resolve a Library. Source is deliberately separate from Content Provider: acquisition and content access are different responsibilities.

## Initial source kinds

The reference implementation supports:

- local directory source;
- Git repository source.

A local source resolves an existing directory. A Git source identifies a repository plus an optional ref and can be materialized into a runtime-managed cache.

## Extensibility

Future source adapters may include package registries, OCI artifacts, object storage manifests, or remote services. The specification does not require a closed enumeration of source kinds.

## Source versus Provider

A source answers "how do I obtain this Library instance?". A provider answers "how do I access this Library's capabilities once resolved?". A Git source may materialize a local checkout whose content is then served by a filesystem content provider; a remote source may instead resolve directly to a remote provider.
