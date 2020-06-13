Ansible Role: Docker setup
=========
A simple role to run [telegraf](https://www.influxdata.com/time-series-platform/telegraf/) in a docker containers. 
The container will be in a dedicated  Docker Bridge network, to keep the service isolated.
The role has been tested on Rasperry Pi only, but it should work on any other Linux machine.

Requirements
------------

Docker must be installed and running on the target hosts. Docker can be installed using the [docker_setup role](https://github.com/ellolo/ansible-docker_setup). 
InfluxDB must be installed and running on a host in order to push logs to it. InfluxDB can be installed as a docker container using the [docker_influxdb_grafan rolea](https://github.com/ellolo/ansible-docker_influxdb_grafana). 

Role Variables
--------------

- ``telegraf_conf_dir``: directory on host machine where telegraf config file will be stored.
- ``telegraf_network``: name of Bridge network that will be created.
- ``telegraf_data_volume``: name of data volume for Telegraf.
- ``telegraf_restart_policy``: restart policy for Telegraf docker container.

Refer to ``defaults/main.yml`` for default values for these variables.

The Telegraf [configuration file](https://github.com/influxdata/telegraf/blob/master/docs/CONFIGURATION.md) is created by this role via Jinja using the template file ``template/telegraf.conf.j2``. Please refer to ``defaults/main.yml`` for an example on how to create the configuration file.
 

Dependencies
------------

None

License
-------

MIT
