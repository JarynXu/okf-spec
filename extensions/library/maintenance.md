# Maintenance Contract

Library consumption and Library maintenance are distinct capability surfaces.

## Consumption

Consumers use the runtime-facing catalog, namespace, read, and query capabilities. Consumers SHOULD NOT mutate provider storage directly.

## Maintenance

Maintenance implementations may expose operations such as:

- create or update knowledge nodes;
- append history;
- invalidate derived knowledge;
- refresh indexes and catalogs;
- update source/revision metadata;
- validate consistency.

A runtime MAY grant maintenance capabilities only to trusted callers. Read-only mounts remain valid Libraries.

## OKF maintenance

For OKF-backed Libraries, maintenance should preserve OKF Core semantics and provenance. The Library Extension does not require every Library to be writable: remote and generated Libraries may be read-only or may delegate maintenance to an external system.
