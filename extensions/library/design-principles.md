# Design Principles

1. **Abstract stable capabilities, not today's technologies.** Storage and transport implementations are adapters.
2. **Preserve Library autonomy.** A domain Library owns its semantic catalog and retrieval guidance.
3. **Separate acquisition, runtime access, and maintenance.** Source, Provider, and Maintenance are distinct responsibilities.
4. **Keep knowledge addresses logical.** Namespace nodes may be physical or virtual.
5. **Prefer deterministic retrieval before expensive retrieval.** Exact/structured lookup may escalate to semantic or agentic strategies when needed.
6. **Preserve evidence and provenance.** Generative retrieval does not remove the requirement to identify knowledge sources.
7. **Make dynamic state derived.** Global catalogs and runtime status are generated from mounted Libraries rather than manually synchronized.
8. **Keep OKF Core compatibility.** Library is an additive extension, not a competing knowledge format.
