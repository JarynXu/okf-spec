# Agentic Query Profile

An Agentic Query Provider may perform multi-step navigation and retrieval inside one or more scopes delegated by the runtime.

It should receive the caller query, Library catalog/navigation data, allowed capabilities, and evidence requirements. It may issue repeated exact, structured, semantic, or graph retrieval operations before returning a standard Query Result.

The provider MUST identify evidence URIs used for synthesized claims and SHOULD expose bounded provenance describing retrieval steps without requiring disclosure of private chain-of-thought. It MUST NOT gain maintenance capabilities merely because it can query a Library.
