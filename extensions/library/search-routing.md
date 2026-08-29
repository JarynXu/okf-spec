# Search Routing

Global query routing is progressive. The runtime first uses caller scope, Library identity, and global catalog metadata to select candidate Libraries. Each selected Library then owns its internal navigation and retrieval strategy through its declared query capabilities.

This prevents the host from needing domain-specific knowledge such as where XCAP or IWF live inside an MCX Library. That expertise belongs to the Library catalog and query provider.
