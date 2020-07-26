# pxeHost Role
This role servers 1 or more functions:
1. Provides dhcp reservations for clients and pxe boot server relay, this would be part of distributed model
2. Provides installation and pxe file hosting for pxe booting systems

# Deployment:
1. all in one:
- dnsmasq is configured as tftp server and hosts all content, when provision playbook runs it configures dhcp reservation here and configures pxe boot files on the local systems hosting services.

# Variables:
1. all in one
- pxeHostOsMedia
  * Dictionary value with each entry containing key value pairs for: 
  * pxeHostDistroName (name for the install media used for file path)
  * pxeHostIsoUrl (http/s path to the iso file for the distrobution)
- pxeHostDhcpScopeStart
  * describes the starting ip to hand our addresses at for dhcp
- pxeHostDhcpScopeStop
  * describes the starting ip to hand our addresses at for dhcp
- pxeHostDhcpScopeNetmask
  * netmask of the pxe host
- pxeHostDhcpScopeGateway
  * gateway of the pxe host
- pxeHostDhcpScopeDns1
  * first dns server of the pxe host
- pxeHostDhcpScopeDns2
  * first dns server of the pxe host
- pxeHostInstallPath
  * path on the pxe host that contains the files for pxe booting and web hosted files
- pxeHostServerIp
  * ip address of the server hosting files
- pxeHostEthernetInterfaceName
  * ethernet nic name to be used in configurations

# Example Playbook (All in one):
```
---
- hosts: '{{ target }}'
  roles:
    - pxeHost
```
