# Examples

The examples below are illustrative and intentionally avoid freezing a serialization format before the reference implementation has validated the model.

## Local Library

A local Library resolves its content directly from a directory. The runtime mounts the Library's semantic catalog and content namespace without copying the source.

## Git Library

A Git-backed Library records a repository source and a selected ref. Installation materializes a local checkout or cache; mounting exposes the resolved revision through the same Library contract used by a local Library.

## Virtual Library

A virtual Library may have no knowledge files on disk. Its provider can generate catalog entries and node contents at read time. For example, a project-context Library may expose a `status` node generated from repository state, while an object-storage Library may expose only lightweight metadata locally and fetch large content on demand.

## Mixed Library

A single Library may compose providers: catalog metadata from Git, raw content from object storage, semantic retrieval from a remote service, and optional agentic retrieval for complex questions. Callers still see one Library identity and one virtual namespace.
