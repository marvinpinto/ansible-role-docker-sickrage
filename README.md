docker-sickrage
===============

[![Build Status](https://img.shields.io/travis/marvinpinto/ansible-role-docker-sickrage/master.svg?style=flat-square)](https://travis-ci.org/marvinpinto/ansible-role-docker-sickrage)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-docker--sickrage-blue.svg?style=flat-square)](https://galaxy.ansible.com/marvinpinto/docker-sickrage)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.txt)

Ansible Galaxy role to manage and run a [sickrage](https://sickrage.github.io)
docker container.

This role wires together the sickrage [docker
container](https://hub.docker.com/r/linuxserver/sickrage) created by
[linuxserver](https://github.com/linuxserver/docker-sickrage), along with
various boilerplate to get things going.


Requirements
------------

This role has been tested on Ubuntu 14.04 and will likely only work on an
Ubuntu-like system. You will also need a functioning docker environment and a
recent-is version of `docker-py` for this role to work.

If you have neither and would like ansible to set this up for you, have a look
at the [marvinpinto.docker](https://galaxy.ansible.com/marvinpinto/docker)
Galaxy role.


Role Variables
--------------

```yaml
# Sickrage host port
docker_sickrage_exposed_port: '8081'

# Docker container name
docker_sickrage_container_name: 'sickrage'

# Directory that will be used as the root of all sickrage-related configuration
# & data. Note that these sub-directories *will* be automatically created if
# they don't already exist.
#
# Assuming 'docker_sickrage_mounted_directory' is set to: /tmp/sickrage_mount
# /tmp/sickrage_mount/config
# /tmp/sickrage_mount/raw_tv_downloads
# /tmp/sickrage_mount/tv
docker_sickrage_mounted_directory: '/tmp/sickrage_mount'
```


Examples
--------

Install this module from Ansible Galaxy into the './roles' directory:
```bash
ansible-galaxy install marvinpinto.docker-sickrage -p ./roles
```

Use it in a playbook as follows:
```yaml
- hosts: '127.0.0.1'
  roles:
    - role: 'marvinpinto.docker-sickrage'
      become: true
```


Mounted Directory
-----------------

The reasoning behind storing all related configuration in the
`docker_sickrage_mounted_directory` root directory is because a person now has
the ability to manage all the configuration + data outside of Ansible.

This becomes especially useful when said mounted directory resides on a
separate filesystem (EBS, USB disk, etc).
