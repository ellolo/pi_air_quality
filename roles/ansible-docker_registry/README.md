Ansible Role: Docker registry
=========
A role to setup an insecure docker registry which will be accessed via unencrypted HTTP connection.
The role also setups all hosts to access the created registry.

Requirements
------------

Docker must be installed and running on all hosts. Docker can be installed using the [docker_setup role](https://github.com/ellolo/ansible-docker_setup). 

The inventory file must have a group called ``docker_registry``, containing the host name or IP of the host where the registry will be installed.

Role Variables
--------------

- ``docker_registry_dir``: directory on the host that will host the registry where registry data will be stored.
- ``docker_registry_restart_policy``: docker registry service restart policy.
- ``docker_registry_url``: url for the docker registry, including port.

Refer to ``defaults/main.yml`` for default values for these variables.

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: raspberries
  
  vars:
    - docker_registry_dir: "/var/lib/registry"
    - docker_registry_restart_policy: always 
    - docker_registry_url: myhost.mynetwork:5000
  roles:
    - role: ansible-docker_setup
    - role: ansible-docker_registry
``` 

License
-------

MIT
