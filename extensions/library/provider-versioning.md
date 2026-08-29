# Provider Versioning

Provider protocol/capability versions are independent from Library knowledge versions. A runtime should negotiate or validate provider capability versions before use and return unsupported-capability or incompatible-provider diagnostics rather than guessing compatibility.

The initial in-process Rust reference implementation uses compile-time trait compatibility. Remote provider protocol version negotiation is reserved for a future transport profile.
