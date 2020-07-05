Use QEMU instead of virtualbox. Virtualbox stops with nested proxmox vm.

## create bridge

Do not use macvtab for your vm network!
Otherwise host to guest communication and dhcp communication inside nested vm is not working.

`vlan40: Network interface to bridge`

`vlan40br: Bridge name`

```
sudo ip link add name vlan40br type bridge
sudo ip link set vlan40br up
sudo ip link set vlan40 master vlan40br
```
