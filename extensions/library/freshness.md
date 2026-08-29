# Freshness

Freshness is provider- or profile-defined state indicating whether derived or cached knowledge is known to correspond to its authoritative source revision.

The generic Library model supports revision and freshness metadata but does not force every Library to have a source revision. Dynamic profiles such as Project Context SHOULD use explicit revisions and invalidation rules. Static or remote Libraries may use version, ETag, timestamp, TTL, or provider-specific signals.
