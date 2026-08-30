# Virtual Filesystem Adapter Profile

Status: Draft v0.1

## Purpose

A filesystem adapter projects the active virtual knowledge namespace into an operating-system filesystem without changing Library identity or assuming that knowledge nodes are physical files.

The adapter is presentation infrastructure. It is not part of the normative Library domain model.

## Projection

A read-only reference projection SHOULD expose mounted Libraries as top-level directories:

```text
<mount>/
  <library-id>/
    <logical-path>...
```

Reading `<mount>/<library-id>/<logical-path>` is equivalent to reading the canonical URI:

```text
okf://<library-id>/<logical-path>
```

Directory enumeration delegates to the owning Library `list` capability. File reads delegate to `read` and MAY therefore hydrate remote, generated, database-backed, or agent-produced content on demand.

## Behavior

- The projection MUST be read-only unless an explicit maintenance capability/profile is separately defined.
- Mounted Library changes SHOULD become visible without changing canonical URIs.
- A Library that cannot provide `list` and `read` cannot be projected as a normal hierarchical filesystem.
- Adapter-specific inode/cache identifiers MUST NOT become knowledge identifiers.
- Errors from providers MUST be mapped to appropriate filesystem errors without fabricating content.

## Platforms

Equivalent implementations may use Linux FUSE, macOS FSKit, Windows ProjFS/WinFSP, or another native virtual-filesystem technology. Platform mechanics are adapters over the same logical projection.

## Security

Mounting a namespace does not increase provider authority. The filesystem host MUST enforce the same process/network/credential policy that applies to normal Runtime reads.
