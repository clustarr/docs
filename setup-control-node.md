# setup control node


## Prepare installation
Download `Ubuntu Server 20.04 LTS` from `https://ubuntu.com/download/server` and start the installation


## Choose Language
Select `English`

![](./images/setup-control-node/1.png)


## Keyboard configuration
Choose `Layout: German` and select `Done`

![](./images/setup-control-node/2.png)


## Network connections
Select `Done`

![](./images/setup-control-node/3.png)


## Configure proxy
Select `Done`

![](./images/setup-control-node/4.png)


## Configure Ubuntu archive mirror
Select `Done`

![](./images/setup-control-node/5.png)


## Guided storage configuration
Select `Done`

![](./images/setup-control-node/6.png)


## Storage configuration
Select `Done`

![](./images/setup-control-node/7.png)

Select `Continue`

![](./images/setup-control-node/8.png)


## Profile setup
Choose
```
name: Ansible
servername: controlnode
username: ansible
password: 123456
```

Select `Done`

![](./images/setup-control-node/9.png)


## SSH Setup
Check `Install OpenSSH server`

Select `Done`

![](./images/setup-control-node/10.png)


## Featured Server Snaps
Select `Done`

![](./images/setup-control-node/11.png)


## Installation
Wait for installation complete message

Select `Reboot`

![](./images/setup-control-node/12.png)


## Accept SSH fingerprint
SSh into control node `ssh ansible@192.168.40.100`

type `yes` to accept the fingerprint

type password `123456`

![](./images/setup-control-node/13.png)


## Run ansible playbook
Now you can start the ansible playbook to configure the control node.

`ansible-playbook setup-controlserver.yml -u ansible -K`

type password `123456`

![](./images/setup-control-node/14.png)
