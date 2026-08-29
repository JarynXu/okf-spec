# Versioning and Compatibility

The Library Extension is versioned independently from OKF Core while declaring an explicit compatible OKF Core baseline.

## Compatibility declaration

A Library Extension release MUST state the OKF Core versions it is compatible with. The initial draft targets OKF Core v0.2 semantics.

## Additive rule

Library metadata and runtime capabilities are additive. A valid OKF Core bundle does not become invalid merely because it does not implement the Library Extension.

## Evolution

New optional capabilities may be added in minor extension revisions. Changes that alter the meaning of existing required fields or lifecycle operations require a major extension revision.

## Provider compatibility

Provider implementations should advertise capability and protocol versions separately from Library content versions. A Library content update does not necessarily imply a provider protocol change, and vice versa.
