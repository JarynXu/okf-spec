# Registry and Global Catalog

A Library Registry tracks resolved Library instances and mount state. It is the runtime source of truth for which Libraries participate in a knowledge space.

## Registry responsibilities

- register and unregister Library instances;
- mount and unmount Libraries;
- expose Library identity, capabilities, source/revision metadata, and status;
- route logical knowledge URIs to the owning Library;
- aggregate semantic catalogs while preserving Library boundaries.

## Dynamic global catalog

The global catalog is derived runtime state, not authoritative hand-maintained knowledge. Mounting or unmounting a Library changes the catalog view immediately. A Library contributes its own optimized semantic catalog; the host does not infer domain navigation by recursively listing storage files.

The global catalog may be exposed as an API, CLI view, MCP resource, HTTP representation, or virtual file. It SHOULD be reproducible from the registry and mounted Library catalogs.
