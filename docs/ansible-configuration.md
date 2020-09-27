# Ansible configuration
Some of the default ansible configuration settings must be adjusted to your network. This includes the
[controlserver IP address](#controlserver) and the [Proxmox VE server IP address](#proxmox). The other settings can be
kept if the instructions have been followed exactly as described before.

The files described here are located relatively to the cloned ansible repository.

## Controlserver
The controlserver host and password can be adjusted in the `inventory/hosts.ini` file.

The IP address or hostname of the controlserver can be specified inside the `[controlserver]` section.
If your controlserver has the IP address `192.168.40.180` then the entry looks like this:

    [controlserver]
    192.168.40.180

The SSH password `ansible_ssh_pass` and the sudo password `ansible_become_password` can be specified inside the
`[controlserver:vars]` section.
If your password is set to `123456` then the entry looks like this:

    [controlserver:vars]
    ansible_ssh_pass=123456
    ansible_become_password=123456

## Proxmox VE

### Host and password
The Proxmox VE server host and password can be adjusted in the `inventory/hosts.ini` file.

The IP address or hostname of the Proxmox VE server can be specified inside the `[proxmox]` section.
If your Proxmox VE server has the IP address `192.168.40.190` then the entry looks like this:

    [proxmox]
    192.168.40.190

The SSH password `ansible_ssh_pass` can be specified inside the `[controlserver:vars]` section.
If your password is set to `123456` then the entry looks like this:

    [proxmox:vars]
    ansible_ssh_pass=123456

### API credentials
The credentials for the API access can be adjusted in the `group_vars/all` file.

The following parameters are required.

- `proxmox_api_user`:
Specifies the user for the API authentication.
This value is visible in the Proxmox VE webinterface in the top right corner.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-api_user).

- `proxmox_api_pass`:
Specifies the password for the API authentication.
This is the same password as the password for the Proxmox VE webinterface.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-api_password).

- `proxmox_api_node`:
Specifies the Proxmox VE node, where the new VM will be created.
This value is visible in the Proxmox VE webinterface inside the datacenter overview.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-node).

The default entry looks like this:

    proxmox_api_user: root@pam
    proxmox_api_pass: "123456"
    proxmox_api_node: pve

### VM hardware
The settings that define the hardware of the VM can be adjusted in the `group_vars/all` file.

The following parameters can be adjusted.

- `proxmox_vm_storage`:
Specifies the storage identifier where to create the virtio hard disk.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-virtio).

- `proxmox_vm_storage_capacity`:
Specifies the size of the virtio hard disk in GB.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-virtio).

- `proxmox_vm_sockets`:
Specifies the number of CPU sockets.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-sockets).

- `proxmox_vm_cores`:
Specifies the number of CPU cores per socket.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-cores).

- `proxmox_vm_memory`:
Specifies the memory size in MB.
More info [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#parameter-memory).

This example entry specifies VMs with a 40GB hard disk, 1 socket, 4 cores and 3GB memory:

    proxmox_vm_storage: local-lvm
    proxmox_vm_storage_capacity: 40
    proxmox_vm_sockets: 1
    proxmox_vm_cores: 4
    proxmox_vm_memory: 3072

## Node passwords
The hashed password for a new node is specified in the file `/roles/pxe/templates/cloud-init/user-data.yml.j2` within 
`autoinstall.identity.password`. To set a new password you have to replace the default value with the hash of your new
password.

To generate the hash for the password `123456` use the following command.

    python3 -c 'import crypt; print(crypt.crypt("123456"))'

Replace `123456` with your desired password.

## Update software
The versions, urls and checksums for the software that will be downloaded while installing the controlserver can be
adjusted in the `group_vars/all` file.

### Proxmox
If you install a Proxmox VE version that is not based on debian buster or the package repository url has changed for
any other reason, you have to adjust the following values.

- `proxmox_enterprise_repository`:
Specifies the package for the enterprise repository.

- `proxmox_no_subscription_repository`:
Specifies the package for the no-subscription repository.

The entry for Proxmox VE 6.2 looks like this:

    proxmox_enterprise_repository: "deb https://enterprise.proxmox.com/debian/pve buster pve-enterprise"
    proxmox_no_subscription_repository: "deb http://download.proxmox.com/debian/pve buster pve-no-subscription"

### kubectl
This section describes how to specify the kubectl release that is installed on the controlserver.

- `kubectl_version`:
Specifies the kubectl version. It can be requested
[here](https://storage.googleapis.com/kubernetes-release/release/stable.txt).

- `kubectl_url`:
Specifies the url to the kubectl release. The version is inserted into the url automatically.

- `kubectl_checksum`:
Specifies the checksum type and value of the kubectl release and can be requested from the url
`https://storage.googleapis.com/kubernetes-release/release/{{ kubectl_version }}/bin/linux/amd64/kubectl.sha256` where
`{{ kubectl_version }}` has to be replaced by the kubectl version (for example
[v1.18.6](https://storage.googleapis.com/kubernetes-release/release/v1.18.6/bin/linux/amd64/kubectl.sha256)).

An example entry looks like this:

    kubectl_version: v1.18.6
    kubectl_url: "https://storage.googleapis.com/kubernetes-release/release/{{ kubectl_version }}/bin/linux/amd64/kubectl"
    kubectl_checksum: sha256:62fcb9922164725c7cba5747562f2ad2f4d834ad0a458c1e4c794cc203dcdfb3

### Ubuntu Server
This section describes how to specify the Ubuntu Server release that is installed on new hosts.

- `ubuntu_server_url`:
Specifies the url to the Ubuntu Server release. It can be requested [here](http://releases.ubuntu.com/20.04/).

- `ubuntu_server_checksum`:
Specifies checksum type and value of the Ubuntu Server release and can be requested
[here](https://releases.ubuntu.com/20.04/SHA256SUMS).

An example entry looks like this:

    ubuntu_server_url: http://releases.ubuntu.com/20.04/ubuntu-20.04.1-live-server-amd64.iso
    ubuntu_server_checksum: sha256:443511f6bf12402c12503733059269a2e10dec602916c0a75263e5d990f6bb93

### RKE
This section describes how to specify the RKE release that is installed on the controlserver.

- `rke_version`:
Specifies the RKE version. It can be requested [here](https://github.com/rancher/rke/releases).

- `rke_url`:
Specifies the url to the RKE release. The version is inserted into the url automatically.

- `rke_checksum`:
Specifies checksum type and value of the RKE release and can be requested
[here](https://github.com/rancher/rke/releases).

An example entry looks like this:

    rke_version: v1.1.4
    rke_url: "https://github.com/rancher/rke/releases/download/{{ rke_version }}/rke_linux-amd64"
    rke_checksum: sha256:1c7bb6e7eb3c820475b3ecbc4fc5786a912658b9d0e1f4323759c1bb72d6a758

### Docker Compose
This section describes how to specify the Docker Compose release that is installed on the controlserver.

- `docker_compose_version`:
Specifies the Docker Compose version. It can be requested [here](https://github.com/docker/compose/releases).

- `docker_compose_url`:
Specifies the url to the Docker Compose release. The version is inserted into the url automatically.

- `docker_compose_checksum`:
Specifies checksum type and value of the Docker Compose release and can be requested
[here](https://github.com/docker/compose/releases).

An example entry looks like this:

    docker_compose_version: 1.26.2
    docker_compose_url: "https://github.com/docker/compose/releases/download/{{ docker_compose_version }}/docker-compose-Linux-x86_64"
    docker_compose_checksum: sha256:13e50875393decdb047993c3c0192b0a3825613e6dfc0fa271efed4f5dbdd6eb
