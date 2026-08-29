# Semantic Ownership

The Runtime owns composition mechanics; each Library owns the semantics of its own knowledge organization. The host may aggregate catalogs and route queries but should not synthesize a domain hierarchy by inspecting filenames alone.

This separation lets a specialized Library encode its optimized topic map, aliases, search hints, and preferred retrieval strategies while remaining pluggable into a generic host.
