# Setup Proxmox VE

## Installation
Download the Proxmox VE ISO image file from [here](https://www.proxmox.com/de/downloads/category/iso-images-pve) and start the installation.

### Boot
![](./assets/images/setup-proxmox/1.png)

Select `Install Proxmox VE`.

### EULA
![](./assets/images/setup-proxmox/2.png)

Accept the end user license agreement.

### Target harddisk
![](./assets/images/setup-proxmox/3.png)

Select the target harddisk.

### Location and Timezone
![](./assets/images/setup-proxmox/4.png)

Choose the country, timezone and keyboard layout.

### Password and E-Mail Address
![](./assets/images/setup-proxmox/5.png)

Choose a password, confirm it and choose an email address.

The default password in the ansible configuration is `123456`.
If you choose a different password here, you have to adjust it in the
[ansible configuration](ansible-configuration.md#host-and-password) too.

### Network configuration
![](./assets/images/setup-proxmox/6.png)

Specify the network configuration.
Make sure that the Proxmox VE host is in the same network as the controlserver.

This IP address must be adjusted in the ansible configuration later.
More info [here](ansible-configuration.md#proxmox).

### Summary
![](./assets/images/setup-proxmox/7.png)

Confirm the summary to start the installation.

### Reboot
![](./assets/images/setup-proxmox/8.png)

Remember the ip address and port. Reboot the system.

## Access the webinterface (optional)
![](./assets/images/setup-proxmox/9.png)

Connect to the shown address (here `https://192.168.40.190:8006/`) and accept the self signed certificate.

![](./assets/images/setup-proxmox/10.png)

Login using user `root` and the password specified before.
