# Initial Acceptance Criteria

The first Library Extension implementation is complete when all of the following hold:

- the Rust SDK exposes storage-independent Library domain types and provider traits;
- a registry can register, mount, unmount, enumerate, and route multiple Libraries;
- a local directory Library can expose an OKF bundle through the Library interfaces;
- a Git source can be described and resolved/materialized without changing upper-layer APIs;
- a purely virtual provider can expose catalog and content without physical knowledge files;
- catalogs from mounted Libraries can be aggregated into a global catalog;
- query dispatch supports deterministic provider selection and a portable evidence-bearing result;
- the CLI exposes Library list/mount/unmount/catalog/read/query operations through the SDK;
- MCP can expose the same logical operations without reimplementing domain logic;
- tests exercise Local, Git-source metadata, and Virtual profiles;
- documentation explains that Project Context is a Library profile, not a separate framework.
