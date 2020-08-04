# Vault Role
0. Best Practices
    * Manual run of first cluster to act as transit engine for unsealing additional clusters
    * unseal keys of transit cluster protected by gpg keys
    * Quantity of keys for unseal distributed amongst trusted parties and multiple keys requried for unseal
    * administrative token generated for trusted parties
    * audit log enabled by root token and unable to be disabled by administrative token
    * root token destroyed after initial configuration and regenerated via unseal keys when required.
    * secondary clusters can be automated once transit keys have been generated for cluster.
1. install vault
    * add repo
    * install vault
2. Configure Vault
    * set permissions on directories
    * configure vault.hcl
        - shamir
        - transit: keyname and token
3. Initialize Vault
    * generate gpg key if requried
    * api call to init
        - root token, unseal / recovery keys
    * unseal cluster
4. add cluster members
    * check status
    * join to cluster
5. Additional configuration
    * audit log enabled
    * administrative token generated
    * administrative policy generated
    * root token destoryed
6. User configuration
    * enable auth methods
    * generate user policies
7. Engine Configuration
    * enable engines
    * configure engines