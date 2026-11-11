**docker_engine**
==============

An Ansible role to install Docker Engine from the official Docker APT repository on Debian and configure `/etc/docker/daemon.json`.

Requirements
------------

- Debian (amd64).
- Ansible Core 2.18 or newer.
- Root access on the managed host.
- Network access to `download.docker.com`.

Role Variables
--------------

| Variable | Default | Description |
|---|---|---|
| `docker_engine_user` | `""` | User added to the `docker` group. Empty: no user is added. |
| `docker_engine_log_max_size` | `"20m"` | Maximum size of a log file (`local` log driver). |
| `docker_engine_log_max_file` | `"5"` | Number of log files kept per container. |
| `docker_engine_log_compress` | `"true"` | Compress rotated log files. |
| `docker_engine_address_pools` | `[{base: "172.20.0.0/16", size: 24}]` | Address pools for networks created without `--subnet`. Empty list: key omitted. |
| `docker_engine_metrics_addr` | `""` | Address of the metrics endpoint. Empty: key omitted. |
| `docker_engine_data_root` | `""` | Docker data directory. Empty: key omitted. |
| `docker_engine_no_new_privileges` | `false` | Set `no-new-privileges` for all containers. |

`live-restore` is never set (incompatible with Swarm mode).
Changing `daemon.json` restarts Docker, and existing containers keep their former logging settings until re-created.

Dependencies
------------

No additional Ansible roles or collections are required.

Example Playbook
----------------

```yaml
---
- name: Install Docker
  hosts: debian
  become: true

  roles:
    - role: docker_engine
      vars:
        docker_engine_user: docker
```

License
-------

MIT

Author Information
------------------

TheWolfPaws
