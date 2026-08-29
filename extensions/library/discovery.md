# Discovery

Discovery answers which Library identities are available to a runtime. The initial reference implementation supports explicit registration and configured sources. Network-wide discovery is outside the first extension profile.

Discovery data may come from configuration, a registry file, a package manager, or a remote catalog adapter. Discovery does not imply mounting: the runtime decides which discovered Libraries become active in the current knowledge space.
