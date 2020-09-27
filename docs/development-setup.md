# Development setup

This document contains setup recommendations for development environments.

## Virtualization

### Hypervisor
Virtualbox always crashed when used to virtualize Proxmox VE and nested VMs were started.
QEMU should be used instead as it has not caused any problems.

### Networking
QEMU requires a bridge as network interface. An macvtab network interfaces do not work because it blocks the host to
guest communication and DHCP communication inside the nested VM does not work.

For example, [this guide](https://askubuntu.com/a/831881) can be used to create a bridge network interface.

## Clear DNS cache
If you remove a host and add a new host with the same name then it also has the same hostname.
This can cause problems because your local DNS cache probably still has the old IP address assigned to the hostname.
Either you create new hosts with different hostnames or you clear the DNS cache manually with the following command.

    sudo systemd-resolve --flush-caches
