# Query Result Contract

This document defines the minimum portable result envelope returned by an OKF Library query provider.

## Goals

A query result must separate generated synthesis from evidence. It must remain useful whether the provider is lexical, semantic, graph-based, remote, or agent-backed.

## Model

A result contains:

- `answer`: optional synthesized text. Deterministic providers may omit it.
- `hits`: zero or more evidence items.
- `provider`: identifier of the provider that produced the result.
- `strategy`: the retrieval strategy actually used.
- `provenance`: optional provider-defined execution provenance.

Each hit contains:

- `uri`: canonical knowledge URI.
- `title`: optional display title.
- `snippet`: optional bounded excerpt.
- `score`: optional provider-local relevance score. Scores are not comparable across providers unless explicitly documented.
- `metadata`: optional structured metadata.

## Evidence rule

Agent-backed or generative providers SHOULD return evidence whenever the answer contains factual claims derived from Library content. A runtime MAY reject synthesized answers that cannot provide evidence when a caller requests evidence-required mode.

## Composition

A runtime may merge results from multiple Libraries. It MUST preserve the originating Library and provider for every hit and MUST NOT normalize provider-local scores into a false global confidence value unless it has an explicit ranking policy.
