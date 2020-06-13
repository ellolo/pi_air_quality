Ansible Role: Docker setup
=========
A simple role to run  [InfluxDB](https://www.influxdata.com/products/influxdb-overview/) and [Grafana](https://grafana.com/) instances
in two separate docker containers. 
The two containers will be in the same Docker Bridge network, to keep the two services isolated.
The role has been tested on Rasperry Pi only, but it should work on any other Linux machine.

Requirements
------------

Docker must be installed and running on all hosts. Docker can be installed using the [docker_setup role](https://github.com/ellolo/ansible-docker_setup). 

Role Variables
--------------

- ``influxdb_conf_dir``: directory on host machine where influxdb [config file](https://docs.influxdata.com/influxdb/v1.8/administration/config/) will be stored. 
- ``monitoring_network``: name of Bridge network that will be created.
- ``influxdb_data_volume``: name of data volume for InfluxDB.
- ``influxdb_restart_policy``: restart policy for InfluxDB docker container.
- ``influxdb_auth_enabled``: set auth-enabled (see [InfluxDB config](https://docs.influxdata.com/influxdb/v1.8/administration/config/)).
- ``influxdb_address``: "influxdb"
- ``grafana_data_volume``: name of data voline for Grafana.
- ``grafana_admin_user``: sets admin user for Grafana.
- ``grafana_admin_pwd``: sets admin password for Grafana.
- ``grafana_allow_embedding``: allow embeddings in Grafana panels (env variable [GF_SECURITY_ALLOW_EMBEDDING](https://grafana.com/docs/grafana/latest/installation/configuration/).
- ``grafana_auth_anon_enable``: allow anonymous access to Grafana without login. This is required for embeddings ([GF_AUTH_ANONYMOUS_ENABLED](https://grafana.com/docs/grafana/latest/auth/overview/))
- ``grafana_disable_sanitized_html``: allow non sanitized html. This is required for iframe embeddings ([GF_PANELS_DISABLE_SANITIZE_HTML](https://grafana.com/docs/grafana/latest/installation/configuration/))). 
- ``grafana_reporting_enabled``: disables reporting.
- ``grafana_restart_policy``: restart policy for Grafana docker container.

Refer to ``defaults/main.yml`` for default values for these variables.

Dependencies
------------

None

Example Playbook
----------------
- hosts: localhost
  
  vars:
    - influxdb_conf_dir: "/home/ansible/influxdb-conf"
    - monitoring_network: "monitoring"
    - influxdb_data_volume: "influxdb-volume"
    - influxdb_restart_policy: "always"
    - influxdb_auth_enabled: "false"
    - influxdb_address: "influxdb"
    - grafana_data_volume: "grafana-volume"
    - grafana_admin_user: "admin"
    - grafana_admin_pwd: "admin"
    - grafana_allow_embedding: "true"
    - grafana_auth_anon_enable: "true"
    - grafana_disable_sanitized_html: "true"
    - grafana_reporting_enabled: "false"
    - grafana_restart_policy: "always"
  roles:
    - role: geerlingguy.pip
    - role: ansible-docker_setup
    - role: ansible-docker_influxdb_grafana

License
-------

MIT
