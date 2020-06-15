# Title

Explain the overall setting and architecture, e.g. influxdb, bridge networks, etc.

## Prerequisite

1. Python3 and git are installed on all machines.
2. Ansible is installed on the control node.

## Usage


1. Install required roles on the control node:

```
ansible-galaxy install -r requirements.yml --roles-path ./roles
```

2. Configure ``inventory`` file as needed. Note that in the provided ``inventory`` file the control node is also the managed node that runs most of the tooling (e.g. InfluxDB, Grafana).

3. Change default variables as defined in playbooks and in ``./roles/*/defaults/main.yml`` to accomodate your deployment, e.g. set hostnames.

4. Perform basic setup of managed nodes, e.g. enabling i2c, setting up required users: 

```
ansible-playbook playbook_machines_setup.yml
```

5. Install docker on all nodes and insecure docker registry on the node in the  ``docker_registry`` group: 

```
ansible-playbook playbook_docker.yml
```

6. Setup and run InfluxDB and Grafana as docker containers on the node in the ``db`` group, in a dedicate Bridge network:

```
ansible-playbook playbook_db.yml
```

7. Setup and run Telegraf as docker container on all managed nodes from which metrics have to be collected. 
If the playbook is run with the [role default variable file](https://github.com/ellolo/ansible-docker_telegraf/blob/master/defaults/main.yml), then the following metrics will be collected:

- system metrics (Telegraf plugins: cpu, mem, disk, diskio, net, processes, file). These metrics will be collected as soon as the docker container is started.
- weather (i.e. indoor air quality) metrics, collected via BME680 sensor. Please refer to [bme680-data-recorder](https://github.com/ellolo/bme680-data-recorder) for details on what metrics are collected and how.  These metrics will be collected only after step 8 is completed.

With the default variables, the metrics will be shipped and stored in influxDB (via Telegraf output plugin) in two separate databases, one for system metrics and one for weather metrics.

```
ansible-playbook playbook_telegraf.yml
```

8. Run weather metrics collection from BME680 sensor in a docker container. The playbook will clone the [bme680-data-recorder](https://github.com/ellolo/bme680-data-recorder) repository, build the corresponding Docker image, push it to the docker registry, and start containers with that image on all managed nodes equipped with BME680. On each of these node, the container will start logging weather metrics, which will be collected by the Telegraf container setup in stup 7.

```
ansible-playbook playbook_bme680.yml
```




