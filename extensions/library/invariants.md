# Runtime Invariants

- A mounted Library ID is unique within one registry.
- Unmounting a Library removes its routes and catalog contribution without deleting installed source material.
- Uninstalling materialized source requires the Library to be unmounted first or atomically removes the mount.
- A canonical knowledge URI resolves within exactly one Library identity.
- A runtime never bypasses Provider contracts to inspect storage-specific implementation details for routing.
- Global catalog state is derivable from mounted Libraries.
