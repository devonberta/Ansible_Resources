# Systemd-resolved Role
0. Other informaiton around syntax and formatting:
    * Variables, groups and naming of items will be done in camel case in all code. Special characters over time need to be updated as ansible matures upper and lowercase letters are not liekly to change.
    * variables are prefixed with the role name in camel case to make certain the variable name is unique per role.
    * All yaml spacing will be done with 2 spaces for each level of ident.

1. Manages the configuration options of systemd-resolved service:
    * Manages /etc/systemd/resolved.conf
    * Manages state of files related to behaviours the service imposes on the system
2. Variables used:
    * systemdResolvedState:
        - Present: Ensures it is running and enabled
        - Absent: Ensures it is not running and disabled
    * systemdResolvedDns:
        - List of DNS servers manually populated, used when servers are not provided by networkmanager, networkd, or resolvconf
    * systemdResolvedFallbackDns:
        - List of DNS servers used when DNS is not set and no DNS servers are made availbe by other packages
    * systemdResolvedLlmnr:
        - no: do not respond to link local discovery dns packets of neighbors
        - yes: allow neighbors to discover hostnames via link local multicast name resolution
    * systemdResolvedMulticastDns:
        - yes: allow use of multicast traffic for hostname.local format discovery on the network
        - no: do not allow the use of multicast traffic for this use
    * systemdResolvedDnssec:
        - false: Default value validates DNSSEC on servers that support it.
        - true: do not accept results from servers that do not support DNSSEC
    * systemdResolvedDomains:
    * systemdResolvedCache:
    * systemdResolvedDnsStubListener:

3. Example Playbook:
    * Coming soon