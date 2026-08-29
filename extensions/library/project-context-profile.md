# Project Context Library Profile

Status: v0.1 application profile

A Project Context Library is a repository-bound application of the generic OKF Library Runtime. It provides durable, queryable project understanding across sessions, context-window resets, and subagents without introducing a second memory system outside OKF.

## Scope

A conforming Project Context Library SHOULD expose at least the current architecture, constraints, active decisions, component/module responsibilities, and an append-only material history. It MAY expose additional project-owned topics through its normal Library catalog.

Project Context is derived knowledge. Source code, tests, build configuration, issue trackers, and other authoritative project artifacts remain the evidence layer. The Library MUST preserve enough provenance for an Agent to re-open authoritative evidence when stronger verification is required.

## Profile state

The profile has four recovery states:

- `UNINITIALIZED`: no validated Project Context checkpoint exists.
- `VALID`: `validated_revision` equals the authoritative current repository revision and no relevant staged, unstaged, or untracked repository changes are present.
- `DIRTY`: committed repository state or the working tree differs from the validated checkpoint and the affected paths can be established.
- `UNKNOWN`: a prior checkpoint exists but freshness cannot be established safely.

A Runtime or adapter MUST derive these states from repository/profile evidence, not from conversational memory. Working-tree changes are part of freshness: an unchanged `HEAD` alone is insufficient evidence for `VALID`.

## Profile metadata

A v0.1 profile state document contains:

```json
{
  "schema_version": "1",
  "project": "okf-cli",
  "library_id": "project-context",
  "repository": "/workspace/okf-cli",
  "validated_revision": "<git-commit-or-null>",
  "impact_rules": [
    {
      "topic": "okf://project-context/current/architecture",
      "path_prefixes": ["src", "packages", "crates"]
    }
  ]
}
```

The profile state is Runtime-local metadata. It MUST NOT store credentials or secrets and SHOULD NOT be treated as portable Library content because repository installation paths and checkout state are environment-specific.

## Canonical knowledge layout

The following logical layout is RECOMMENDED for the default profile:

```text
okf://<library>/
  current/
    architecture
    constraints
    decisions
    components
  history/
    log
```

`current/` describes the present validated understanding. `history/log` records material evolution and checkpoint history. Implementations MAY add domain-specific nodes and catalog entries.

## Recovery protocol

A new session or subagent SHOULD:

1. resolve the Project Context profile and mounted Library;
2. evaluate freshness against the authoritative repository revision and working tree;
3. if `VALID`, load the semantic catalog and only task-relevant knowledge;
4. if `DIRTY`, compute the committed/working-tree delta and impacted topics, then revalidate those topics before relying on them;
5. if `UNKNOWN`, re-establish repository evidence conservatively before project modification;
6. if `UNINITIALIZED`, bootstrap the Library from authoritative project evidence.

A parent Agent delegating work SHOULD pass the project identity, current revision, relevant Library identity/URIs, and task scope. A child Agent MUST still verify revision compatibility before using inherited context.

## Incremental impact analysis

Project Context SHOULD maintain deterministic mappings from repository paths to knowledge topics. When the repository is `DIRTY`, an adapter computes paths changed by commits since `validated_revision` and by the current working tree, maps those paths to impacted topics, and revalidates only affected knowledge when the impact can be bounded.

Impact rules are hints for invalidation, not proof that unaffected topics remain correct. Cross-cutting changes, dependency upgrades, generated-code changes, migration changes, or failed invariants MAY require broader revalidation.

## Maintenance and checkpoint advancement

After authorized project changes, the maintenance workflow SHOULD:

1. update affected `current/` knowledge;
2. append material decisions/evolution to history;
3. preserve source/evidence references;
4. refresh catalog/index state when required;
5. run project-required source/tests/validation;
6. ensure the intended project and knowledge changes are committed as required by project policy;
7. only then advance `validated_revision` to the verified authoritative revision.

Checkpoint advancement records prior verification. It MUST NOT itself mutate portable knowledge content after selecting the validated revision, because doing so would immediately make that checkpoint stale. Advancing the checkpoint before required verification is complete is non-conformant.

## Runtime boundary

This profile consumes generic Library primitives: namespace, catalog, query, provenance, lifecycle, source, and provider capabilities. Project Context freshness helpers MAY exist in SDKs or CLIs, but they MUST NOT force project-specific branches into the generic Library provider contract.

Project Context therefore validates the Library architecture as an application framework: specialized knowledge behavior is layered on top of the common cartridge/runtime interface rather than bypassing it.
