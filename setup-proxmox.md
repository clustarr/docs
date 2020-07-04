Download Proxmox VE iso

`https://www.proxmox.com/de/downloads/category/iso-images-pve`

Boot from the iso to start the installation.

Select `Install Proxmox VE`

![](./images/setup-proxmox/1.png)

Accept the end user license agreement.

![](./images/setup-proxmox/2.png)

Select the target harddisk.

![](./images/setup-proxmox/3.png)

Choose the country, timezone and keyboard layout.

![](./images/setup-proxmox/4.png)

Choose a password, confirm it and choose an email address.

![](./images/setup-proxmox/5.png)

Specify the network configuration.

![](./images/setup-proxmox/6.png)

Confirm the summary to start the installation.

![](./images/setup-proxmox/7.png)

Remember the ip address and port. Reboot the system.

![](./images/setup-proxmox/8.png)

Connect to the shown address `https://192.168.40.192:8006/` and accept the self signed certificate.

![](./images/setup-proxmox/9.png)

Login using user `root` and the password specified before.

![](./images/setup-proxmox/10.png)






## Notes for virtualbox
Follow this steps:

`https://pve.proxmox.com/wiki/Proxmox_VE_inside_VirtualBox`.

Enable nested virtualization on vm named `proxmox` using the command

`VBoxManage modifyvm proxmox --nested-hw-virt on`
