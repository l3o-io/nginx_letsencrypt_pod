nginx_letsencrypt_pod
=====================

This Ansible role setups nginx and letsencrypt containers using podman.

Role Variables
--------------

| Variable                        | Value                                                                |
| ------------------------------- | -------------------------------------------------------------------- |
| ``nginx_domains``               | list of domains which should get a default page                      |
| ``letsencrypt_domains``         | list of domains to request certificates for                          |
| ``letsencrypt_camail``          | mail address used for requesting certificates                        |
| ``nginx_container_name``        | ``nginx`` (default)                                                  |
| ``letsencrypt_container_name``  | ``certbot`` (default)                                                |
| ``nginx_http_ip``               | host ip address the http port should be bound to (optional)          |
| ``nginx_https_ip``              | host ip address the https port should be bound to (optional)          |
| ``nginx_http_port``             | ``8080`` (default)                                                   |
| ``nginx_https_port``            | ``8443`` (default)                                                   |
| ``nginx_rootdir``               | ``/tmp/nginx`` (default)                                             |
| ``letsencrypt_rootdir``         | ``/tmp/letsencrypt`` (default)                                       |
| ``nginx_webroot``               | ``/usr/share/nginx/html`` (default)                                  |
| ``nginx_confdir``               | ``/etc/nginx/conf.d`` (default)                                      |
| ``nginx_static_config``         | list of directories containing static configuration files (optional) |
| ``nginx_static_site``           | list of directories containing static website directories (optional) |
| ``letsencrypt_confdir``         | ``/etc/letsencrypt`` (default)                                       |
| ``letsencrypt_statedir``        | ``/var/lib/letsencrypt`` (default)                                   |
| ``nginx_container_image``       | ``quay.io/cfelder/nginx:stable-www-data (default)                    |
| ``letsencrypt_container_image`` | ``docker.io/certbot/certbot:latest (default)                         |
| ``podman_network_name``         | ``podman`` (default)                                                 |
| ``container_state``             | ``present`` (default) or ``absent``                                  |

Dependencies
------------

* [ikke_t.podman_container_systemd](https://galaxy.ansible.com/ikke_t/podman_container_systemd)

Example Playbook
----------------

The following playbook setups nginx and letsencyrpt containers for ``www.example.com``:

    - name: Setup nginx and letsencrypt containers
      hosts: all
      tasks:
        - include_role:
            name: nginx_letsencrypt_pod
          vars:
            nginx_rootdir: "/tmp/nginx_ex"
            letsencrypt_rootdir: "/tmp/letsecnrypt_ex"
            letsencrypt_camail: "ca@example.com"
            nginx_http_port: "80"
            nginx_https_port: "443"
            nginx_domains:
              - "www.example.com"
            letsencrypt_domains: "{{ nginx_domains }}"

License
-------

GPLv3+

Author Information
------------------

Christian Felder
