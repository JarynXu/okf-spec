# Reference Test Matrix

The implementation validation matrix covers:

| Capability | Local | Git | Virtual |
| --- | --- | --- | --- |
| identity/manifest | required | required | required |
| catalog | required | required | required |
| namespace list/read | required | required after resolution | required |
| query | required | required after resolution | required |
| mount/unmount | required | required | required |
| physical files required | yes | materialized source | no |

The virtual profile is an architectural guardrail: if tests require direct filesystem access in the runtime core, the implementation violates the Provider abstraction.
