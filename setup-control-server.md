# setup control node


## Prepare installation
Download `Ubuntu Server 20.04 LTS` from `https://ubuntu.com/download/server` and start the installation.


## Installation

### Choose Language
Select `English`

![](./images/setup-control-server/1.png)


### Keyboard configuration
Choose `Layout: German` and select `Done`

![](./images/setup-control-server/2.png)


### Network connections
Select `Done`

![](./images/setup-control-server/3.png)


### Configure proxy
Select `Done`

![](./images/setup-control-server/4.png)


### Configure Ubuntu archive mirror
Select `Done`

![](./images/setup-control-server/5.png)


### Guided storage configuration
Select `Done`

![](./images/setup-control-server/6.png)


### Storage configuration
Select `Done`

![](./images/setup-control-server/7.png)

Select `Continue`

![](./images/setup-control-server/8.png)


### Profile setup
Choose
```
name: Ansible
servername: controlserver
username: ansible
password: 123456
```

Select `Done`

<!---
TODO: fix servername in image 9.png
-->

![](./images/setup-control-server/9.png)


### SSH Setup
Check `Install OpenSSH server`

Select `Done`

![](./images/setup-control-server/10.png)


### Featured Server Snaps
Select `Done`

![](./images/setup-control-server/11.png)


### Installation
Wait for installation complete message

Select `Reboot`

![](./images/setup-control-server/12.png)


### Run ansible playbook
Now you can start the ansible playbook to configure the control node.

`ansible-playbook setup-controlserver.yml -k -K`

Enter your password.


## Generate new cloud-init password
To generate a new cloud-init password you can use the following command.

```shell
python3 -c 'import crypt; print(crypt.crypt("123456"))'
```
