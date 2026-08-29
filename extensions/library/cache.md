# Cache Semantics

Caching is an implementation concern constrained by freshness and provenance. A runtime may cache catalogs, node contents, source materialization, or query results, but must not present stale cached data as current when a provider exposes a newer known revision.

Providers that can identify revisions should surface them. Cache keys should include Library identity and provider/source revision when available. Providers without revision signals may define TTL or explicit refresh semantics.
