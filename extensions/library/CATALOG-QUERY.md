# Catalog and Query Contracts

Status: Draft

## Catalog is semantic navigation

A Library catalog is not merely a storage directory listing. It describes how a domain expert intends the Library's knowledge to be discovered progressively.

A catalog entry SHOULD be able to carry:

- stable logical identity;
- title and description;
- semantic section or topic;
- aliases or terminology;
- child entry points;
- relationships to other catalog entries;
- preferred query scope or hints;
- references to underlying knowledge nodes.

This allows a specialized Library to teach a generic runtime how to navigate domain knowledge without requiring the runtime to understand that domain.

## Global aggregation

A runtime MAY aggregate each mounted Library's catalog into a global catalog.

Aggregation MUST preserve the originating Library identity and SHOULD avoid flattening all domain knowledge into a single undifferentiated search space.

Progressive discovery should normally follow:

```text
global catalog -> library -> semantic section/topic -> knowledge nodes
```

## Query capabilities

A Library MAY advertise multiple retrieval capabilities, such as:

- `exact`
- `structured`
- `lexical`
- `semantic`
- `graph`
- `remote`
- `agentic`

Capability names and negotiation rules will be versioned before stabilization.

## Query routing

The runtime SHOULD select a Library and then invoke a query capability supported by that Library. It MUST NOT assume one global search algorithm is authoritative for every Library.

A Library MAY define a preferred retrieval cascade. For example:

```text
exact -> structured -> semantic -> agentic
```

The cascade is advisory unless a future version explicitly marks a stage as required.

## Agentic query

An agent-backed query provider is an optional specialized retrieval implementation. It may inspect the Library catalog, run multiple searches, follow references, compare evidence, and return a synthesized result.

Agentic query MUST remain behind the same query contract so callers need not know whether retrieval was lexical, vector-based, remote, or agent-executed.

## Query results

A standard query result envelope SHOULD eventually support:

- answer or retrieved content;
- matched knowledge nodes;
- evidence/provenance;
- originating Library;
- strategy used;
- diagnostics;
- optional confidence or ranking signals.

The exact serialization remains open in this draft.
