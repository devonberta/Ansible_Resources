# bareMetalProvision Role
This role serves the following functions:
1. Create DHCP Reservation for host
2. Create unattend file for installation
3. Create pxelinux cfg file for boot process
4. Manage the pxe boot desired state after installation has been validated

# How this is achieved
1. Host has basic information defined as variables:
- mac addresses in a list format
- hostname
- ip address
- subnet mask
- gateway
- dns server 1
- dns server 2
- operating system
- installation disk
- desired pxe server to perform the installation
- local admin password
- IPMI ip Address
- IPMI username
- IPMI password
2. Templates generated for Host on desired pxe server:
- DHCP Reservation with all mac addresses from mac address list and ip address
- unattend file built from template for desired OS
- pxelinux cfg file matching each mac address in mac address list
3. Host is forced to pxe boot:
- IPMI Command set next boot to pxe
- IPMI Command reboot node
4. PXE Boot Server takes over:
- Role waits for OS to become available
- PXE Server serves DHCP reservation and next server
- PXE Server serves pxelinux.cfg for mac address that responded
- PXE Server serves installation files and unattend file for installation
- OS installs and runs post tasks via unattend file
5. Role detects OS is available
- Connects and performs OS specific custimization if needed
- Role is completed

# Variables:
1. Required:
- bare_metal_provision_mac_address_list
  * A list of mac addresses in xx:xx:xx:xx:xx:xx format, used to create dhcp reservations and name pxelinux files for network boot installation
- bare_metal_provision_hostname
  * hostname that will be applied to the provisioned host
- bare_metal_provision_ip_address
  * ip address that will be used for pxe boot and applied to provisioned host
- bare_metal_provision_subnet_mask
  * the subnet mask of the network the host will be provisioned in
- bare_metal_provision_gateway
  * the gateway of the network the host will be provisioned in
- bare_metal_provision_dns server 1
  * the first dns server of the network the host will be provisioned in
- bare_metal_provision_dns server 2
  * the second dns server of the network the host will be provisioned in
- bare_metal_provision_operating_system
  * the operating system that will be provisoned on the host
- bare_metal_provision_installation_disk
  * the disk that the operating system will be installed on to (/dev/sda)
- bare_metal_provision_pxe_server
  * the ip address of the pxe server that will provide dhcp, pxelinux, installation and unattend files
- bare_metal_provision_pxe_username
  * Username for the pxe server to connect to and configure, dhcp, unattend and pxelinux files
- bare_metal_provision_pxe_server_password
  * Password for the pxe server to connect to and conifgure dhcp, unattend and pxelinux files
- bare_metal_provision_local_admin_password
  * the cleartext value of the local admin password to be set, this is hashed for linux an applied after OS installation has completed in windows
- bare_metal_provision_ipmi_ip_address
  * ip address of the ipmi of the host you are provisioning
- bare_metal_provision_ipmi_username
  * the username of the ipmi interface on the host you are provisioning
- bare_metal_provision_ipmi_password
  * the cleartext password of the ipmi interface username for the host you are provisioning

# Example Playbook (All in one):
```
---
- hosts: '{{ env }}'
  roles:
    - bareMetalProvision
```
ss