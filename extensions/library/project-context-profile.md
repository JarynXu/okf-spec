# Project Context Library Profile

This document is a non-core profile demonstrating how a dynamic project-context knowledge base can be implemented as an OKF Library.

A project-context Library binds derived project knowledge to repository state. It typically exposes architecture, modules, decisions, constraints, workflows, history, and runtime status through the standard Library namespace and query contracts.

Recommended profile metadata includes repository identity, validated revision, source/provenance pointers, and freshness state. When repository state changes, affected derived knowledge should be revalidated or invalidated rather than blindly reused.

Project-context knowledge is consumed through the same Library query interfaces as any other Library. Maintenance may use OKF-aware tooling to update knowledge, provenance, history, and validated revision.

This profile does not add new Runtime primitives; it validates that project context is an application of the generic Library model rather than a separate knowledge system.
