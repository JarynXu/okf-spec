# Architecture Boundary

The Library Extension follows a dependency-inversion model.

The stable domain concepts are Library, manifest, namespace node, catalog, query, lifecycle, and provider capabilities. Storage and transport technologies are adapters around those concepts.

A runtime implementation SHOULD keep domain logic independent from Local, Git, S3, HTTP, database, FUSE, MCP, and agent implementations. Concrete adapters depend inward on capability contracts; core runtime routing does not depend outward on storage-specific types.

This allows one Library to compose multiple adapters while retaining one identity and one virtual knowledge namespace.
