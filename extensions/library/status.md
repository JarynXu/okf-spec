# Runtime Status

Runtime status is derived state and may be exposed through the virtual namespace.

A mounted Library SHOULD be able to report at least its identity, mount state, declared capabilities, source revision when known, and freshness/validation state when the provider can determine it.

Status nodes are allowed to be virtual and generated on read. They are not required to be persisted inside the Library's knowledge content.
