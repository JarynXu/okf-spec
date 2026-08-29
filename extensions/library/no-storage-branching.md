# No Storage Branching Rule

Core runtime code must dispatch by declared capabilities and Library identity. Branches such as `if source == local`, `if source == git`, or `if source == s3` are adapter concerns and are prohibited as the main routing model of the Library Runtime.
