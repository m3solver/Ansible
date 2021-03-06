Role Name
=========

An [Ansible] role to install [Graylog]

Build Status
------------

[![Build Status](https://travis-ci.org/mrlesmithjr/ansible-graylog.svg?branch=master)](https://travis-ci.org/mrlesmithjr/ansible-graylog)

Requirements
------------

Install required [Ansible] roles:
```
sudo ansible-galaxy install -r requirements.yml
```

You **MUST** define the following vars:
```
# Generate new pw using...pwgen -N 1 -s 96
graylog_server_password_secret: []

# Generate new pw using...echo -n yourpassword | shasum -a 256
graylog_server_root_password: []
```

Vagrant
-------
Spin up Environment under Vagrant to test.
````
vagrant up
````

Role Variables
--------------

```
---
# defaults file for ansible-graylog
graylog_config_graylog_server: true

graylog_debian_package_info:
  file: 'graylog-{{ graylog_version }}-repository_latest.deb'
  url: 'https://packages.graylog2.org/repo/packages'

graylog_es_cluster_name: 'graylog'

# Defines if node should be a data node in the cluster...default is true
graylog_es_data_node: true

graylog_es_discovery_zen_ping_unicast_hosts:
  - 'localhost'

# Defines if node should be a master node in the cluster...default is true
graylog_es_master_node: true

graylog_es_network_host: 127.0.0.1

graylog_es_replicas: 0
graylog_es_shards: 4

graylog_group: 'graylog'

# Defines if Java Default JRE is installed
# Best to use oracle-java-8
graylog_install_default_java_jre: false

graylog_message_journal_dir: '/data/journal'
graylog_message_journal_enabled: true

graylog_mongodb_uri: 'mongodb://localhost/graylog'

graylog_redhat_package_info:
  file: 'graylog-{{ graylog_version }}-repository_latest.rpm'
  url: 'https://packages.graylog2.org/repo/packages'

# REST API listen URI. Must be reachable by other Graylog server nodes if you run a cluster
graylog_rest_listen_uri: 'http://127.0.0.1:9000/api/'

# Default is true unless installing multiple instances
graylog_server_master: true

# Generate new pw using...pwgen -N 1 -s 96
graylog_server_password_secret: []

# Generate new pw using...echo -n yourpassword | shasum -a 256
graylog_server_root_password: []

# Define Syslog Input Protocol udp|tcp
graylog_server_syslog_input_protocol: 'udp'

graylog_user: 'graylog'

# Define Graylog Version to Install
graylog_version: 2.2

# Generate new pw using...pwgen -N 1 -s 96
graylog_web_application_secret: 'X4S0oYP9DcGjgpX6uAGOfHS3NbB5OpSHWVKwQP94mJxaDCM3WPP0QP5zd8uqZs2tDBPiKET6r81IJEumQkqAk6WOnqKwvCu1'

# Web interface listen URI.
graylog_web_listen_uri: 'http://127.0.0.1:9000/'
```

Dependencies
------------

Referent requirements section

Example Playbook
----------------

```
---
- hosts: test-nodes
  become: true
  vars:
    es_major_version: '2.x'
    es_minor_version: '2.4.1'
    graylog_rest_listen_uri: 'http://0.0.0.0:9000/api/'
    graylog_web_listen_uri: 'http://0.0.0.0:9000/'
    graylog_version: '2.2'
    pri_domain_name: 'test.vagrant.local'
  roles:
    - role: ansible-timezone
    - role: ansible-oracle-java8
    - role: ansible-elasticsearch
    - role: ansible-mongodb
    - role: ansible-graylog
  tasks:
```

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com

[Ansible]: <https://www.ansible.com>
[Graylog]: <https://www.graylog.org/>
