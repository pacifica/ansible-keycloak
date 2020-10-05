Pacifica Keycloak Ansible Role
==============================

This Ansible role manages a configuration of Keycloak that is specific to Pacifica
services. This role does require Keycloak to use SSL/TLS connections, and does not
have options to disable that (because why?). The default configurations for SSL/TLS
certificates conveniently match the outputs of the defaults for the
[Pacifica CertInfra Ansible Role](https://github.com/pacifica/ansible-certinfra).

Requirements
------------

 * Ansible >= 2.9
 * System SSL Key, Certificate and Chain (PEM format)

Role Variables
--------------

There are a lot of variables in the [default](defaults/main.yml) that I won't
cover here, the basics will be covered here:

  * Version Variables - if you change one, change them all...
    * `keycloak_version` (default: '11.0.2')
    * `keycloak_url` (default: https://downloads.jboss.org/keycloak/{{ keycloak_version }}/keycloak-{{ keycloak_version }}.tar.gz)
    * `keycloak_checksum` (default: sha1:9c870a2fdf7bb44933c23d264ee9a360af4b6a44)
  * Packages and Install
    * `keycloak_packages` (default: ['java-11-openjdk-headless', 'tar', 'gzip'])
    * `keycloak_install_dir` (default: /usr/local/keycloak)
    * `keycloak_install_owner` (default: root)
    * `keycloak_install_group` (default: root)
  * Certificiate, Key and Chain
    * `keycloak_private_key` (default: /etc/pki/tls/private/localhost.localdomain.pem)
    * `keycloak_certificate` (default: /etc/pki/tls/certs/localhost.localdomain.crt)
    * `keycloak_chain` (default: /etc/pki/tls/certs/pacifica_chain.io.crt)
  * Network Configurations
    * `keycloak_service_address` (default: '0.0.0.0')
  * Admin Password
    * `keycloak_admin_password` (default: 'admin')

Dependencies
------------

None

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: pacifica.ansible_keycloak, keycloak_admin_password: 'admin1234' }
```

License
-------

LGPL-v3
