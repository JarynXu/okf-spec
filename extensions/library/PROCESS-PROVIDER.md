# Process Provider Protocol

Status: Draft v1

## Purpose

The process provider protocol lets a Library package ship or reference a dedicated provider program while keeping OKF Runtime implementations language-neutral. It is suitable for dynamic knowledge, specialist retrieval agents, project-state providers, database gateways, and other adapters that cannot be represented as static files.

The protocol is request/response JSON over standard input/output. One invocation handles one request. Hosts MAY add a persistent transport later without changing the semantic request/response model.

## Invocation

The host resolves `command` and `args` from an authorized `kind: process` provider declaration. Relative executable paths and `cwd` values are resolved against the materialized Library root.

The host SHOULD expose these environment variables:

- `OKF_LIBRARY_ROOT`: materialized Library root when one exists;
- `OKF_LIBRARY_ID`: active Library identity;
- `OKF_PROVIDER_ID`: provider declaration identity.

The host MUST NOT forward arbitrary secrets unless deployment policy explicitly authorizes them.

## Request envelope

```json
{
  "protocol": "okf-provider/1",
  "operation": "read",
  "library": "project-context",
  "uri": "okf://project-context/status"
}
```

Common fields:

- `protocol`: MUST be `okf-provider/1`;
- `operation`: one of `catalog`, `list`, `read`, `query`, `refresh`;
- `library`: active Library id.

Operation fields:

- `list`: `path`;
- `read`: `uri`;
- `query`: `query` object compatible with the Library query request model;
- `refresh`: no additional required field.

## Response envelope

Success:

```json
{
  "ok": true,
  "data": {}
}
```

Failure:

```json
{
  "ok": false,
  "error": {
    "code": "provider-error",
    "message": "human-readable diagnostic"
  }
}
```

`data` MUST encode the same semantic object the corresponding Provider capability returns: Library catalog, knowledge-node sequence, UTF-8 content string, query result envelope, or `null` for refresh.

A process MUST write protocol output only to stdout. Diagnostics belong on stderr. Non-zero exit, malformed JSON, mismatched protocol data, or a timeout are provider failures.

## Agent-backed providers

A dedicated Agent MAY implement this protocol. The host gives it only the authority implied by the activated capability. A `query` provider does not implicitly gain `read`, maintenance, shell, or credential authority.

The returned query result MUST preserve evidence/provenance whenever the provider synthesizes an answer.
