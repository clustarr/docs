# Getting started
Clustarr allows easy installation and maintenance of kubernetes clusters.

## Repositories
The clustarr project consists of the following repositories.

### Ansible
The [ansible](https://github.com/clustarr/ansible) repository contains ansible configuration files. They describe
how to set up the controlserver, the Proxmox VE server and how to install and configure new cluster nodes.

### Backend
The [backend](https://github.com/clustarr/backend) repository provides a backend that is running on the controlserver.
It is used by the frontend to provide a REST API to list tasks, execute new tasks (ansible playbooks), cancel tasks,
provide output of tasks and list hosts.

### Frontend
The [frontend](https://github.com/clustarr/frontend) repository provides a webinterface to maintain the cluster.
It communicates with the backend. See [webinterface](webinterface.md) for more info.

### Docs
The [docs](https://github.com/clustarr/docs) repository holds the code for this documentation.
