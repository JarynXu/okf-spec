# HTTP Remote Provider Protocol

Status: Draft v1

## Purpose

The HTTP remote provider profile exposes the same semantic operations as the process provider over an authenticated HTTP boundary. It allows very large or distributed Libraries to remain remote while participating in the same OKF Library Runtime.

## Endpoint

A provider declaration supplies `base_url`. The v1 execution endpoint is:

```text
POST <base_url>/v1/execute
```

The request and response JSON bodies are identical to the Process Provider Protocol envelopes.

Example request:

```json
{
  "protocol": "okf-provider/1",
  "operation": "query",
  "library": "mcx",
  "query": {
    "text": "XCAP document selector",
    "limit": 8
  }
}
```

## Authentication

Portable manifests MUST NOT contain bearer tokens or passwords. A deployment MAY specify a credential environment-variable name or credential slot in adapter configuration. The host resolves the secret at activation time.

Reference clients SHOULD support bearer-token authentication and SHOULD allow unauthenticated endpoints when policy permits.

## Semantics

- `catalog`, `list`, `read`, `query`, and `refresh` have the same semantics as their Library Provider contracts.
- Canonical `okf://` URIs MUST be preserved across the network boundary.
- A server SHOULD return `application/json` and UTF-8.
- Non-2xx responses, invalid envelopes, timeouts, and TLS failures are provider failures.
- Servers SHOULD return bounded query evidence and provenance rather than opaque synthesized text.

## Caching and freshness

HTTP caching is deployment policy. A host MAY use ETag, Last-Modified, or provider provenance to cache results, but MUST NOT silently claim freshness that the remote provider did not establish.
