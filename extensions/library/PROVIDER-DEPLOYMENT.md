# Provider Deployment Profile

Status: Draft v0.2 implementation profile

## Purpose

The Library domain model is capability-oriented. A portable package MAY declare how a deployment can bind concrete provider adapters without making storage or transport kinds part of the Library domain.

Provider declarations are optional deployment metadata. They do not replace OKF knowledge, the semantic catalog, or Runtime policy.

## Manifest form

`okf-library.yaml` MAY contain a `providers` sequence:

```yaml
providers:
  - id: remote-content
    kind: http
    capabilities: [list, read, query, refresh]
    config:
      base_url: https://knowledge.example.com/okf
      token_env: KNOWLEDGE_TOKEN

  - id: specialist-agent
    kind: process
    capabilities: [query]
    config:
      command: ./bin/library-agent
      args: [provider]
```

Each declaration contains:

- `id`: stable deployment-local provider identity;
- `kind`: adapter kind resolved by the host;
- `capabilities`: Library capabilities the adapter is expected to supply;
- `config`: adapter-specific non-secret configuration.

A host MUST validate that the resolved adapter actually supplies every declared capability before mounting the Library.

## Security

Provider declarations are untrusted data. A declaration MUST NOT itself grant process execution, network access, credential access, or write authority.

Hosts MUST apply deployment policy before activating an adapter. In particular:

- executable/process providers require explicit Runtime authorization;
- network providers require explicit network policy;
- credential values MUST NOT be embedded in portable manifests;
- a manifest MAY name an environment variable or runtime credential slot, but the secret value is deployment state;
- provider content remains untrusted knowledge and MUST NOT be interpreted as Agent instructions.

## Composition

Multiple declarations MAY be composed into one Library. For example:

- S3 supplies `list` and `read`;
- the package manifest supplies `catalog`;
- a semantic index supplies `query`;
- a process provider supplies `refresh`.

The Runtime still exposes one Library identity and routes only by capability.

## Adapter kinds

Adapter kind names are deployment identifiers, not additions to the Library domain type system. This repository defines interoperable profiles for `process` and `http`. Reference implementations may additionally provide `s3`, `sqlite`, `semantic-index`, filesystem, or other adapter kinds.

Unknown kinds MUST fail closed unless the host has an explicitly registered adapter for that kind.
