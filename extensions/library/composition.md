# Library Composition

A runtime may mount multiple Libraries and present an aggregated global catalog. Library boundaries remain explicit: identical topic names do not imply merged ownership, and canonical URIs retain the originating Library ID.

Cross-Library query may fan out to eligible mounted Libraries. The runtime may use catalog metadata, namespaces, caller scope, or routing policy to select candidates before invoking Library-specific query providers.

A Library may also declare dependencies on other Library identities in future versions, but dependency semantics are not required for the initial profile.
