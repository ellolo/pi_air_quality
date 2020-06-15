# Title

## Prerequisite

1. Python3 and git are installed on all machines.
2. Ansible is installed on the control node.

## Usage

1. Install required roles on the control node:
```
ansible-galaxy install -r requirements.yml --roles-path ./roles
```

2. Configure ``inventory`` file as needed. Note that in the provided ``inventory`` file the control node is also the managed node that runs most of the tooling (e.g. InfluxDB, Grafana).
3. Perform basic setup of managed nodes, e.g. enabling i2c, setting up required users: ``ansible-playbook playbook_machines_setup.yml``
4. Install docker on all nodes and insecure docker registry on the nodes part of ``docker_registry`` group: 

