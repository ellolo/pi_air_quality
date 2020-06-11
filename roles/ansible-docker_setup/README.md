Ansible Role: Docker setup
=========
A simple role to install [Docker](https://www.docker.com)  on Linux machines. The role has been tested on Rasperry Pi only, but it should work on any other Linux machine.

Requirements
------------

Requires pip to be already installed, if Docker Compose needs to be installed in addition to Docker.

Role Variables
--------------

- ``docker users``: list of users to add to ansible group.
- ``private_network_dns``: IP of the local network DNS. This allows to see localhost.
- ``pip_version``: Pip version to install Docker Compose.
- ``install_docker_compose``: if to install docker compose or not.

Refer to ``defaults/main.yml`` for default values for these variables.

Dependencies
------------

None

Example Playbook
----------------
- hosts: raspberries
  
  vars:
    - docekr_user: foo
    - private_network_dns: 192.168.178.1 
    - install_docker_compose: false
  roles:
    - role: geerlingguy.pip
    - role: ansible-docker_setup
 

License
-------

MIT / BSD
