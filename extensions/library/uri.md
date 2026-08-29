# Knowledge URI

The extension defines a logical URI space independent of any operating-system filesystem path.

The reference form is `okf://<library-id>/<path>`. Implementations MAY expose alternate presentation forms, including CLI paths, HTTP routes, MCP resources, or filesystem mounts, but MUST preserve the same Library identity and logical path semantics.

Library IDs are stable within a registry. Paths are hierarchical, use `/` as the logical separator, and identify namespace nodes rather than necessarily identifying physical files.

A URI can therefore resolve to static Markdown, generated content, a remote object, database-backed knowledge, or another provider-defined node without changing the caller-facing address.
