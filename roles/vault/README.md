# Vault Role
0. Other informaiton around syntax and formatting:
    * Variables, groups and naming of items will be done in camel case in all code. Special characters over time need to be updated as ansible matures upper and lowercase letters are not liekly to change.
    * variables are prefixed with the role name in camel case to make certain the variable name is unique per role.
    * All yaml spacing will be done with 2 spaces for each level of ident.

1. Deploys Hashicorp Vault OSS in clusterd configuration with a number of configurations:
    * Cluster with RAFT storage SHAMIR Unseal method
    * Cluster with RAFT storage and Transit Engine Auto Unseal method
2. Variables used:
    * vaultSoftwareVersion
3. Example Playbook:
    * Coming soon