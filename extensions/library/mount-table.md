# Mount Table

The Runtime maintains a mount table mapping Library identity to an active Library instance and its route prefix. This table is dynamic state analogous to a routing table: it is generated and updated by code as Libraries are mounted and unmounted.

The mount table may be projected into the virtual namespace for inspection. Such a projection is generated runtime content, not an authoritative source file.
