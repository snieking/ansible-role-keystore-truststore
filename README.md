Ansible Role: Keystore Truststore
=========
[![Build Status](https://travis-ci.org/snieking/ansible-role-keystore-truststore.svg?branch=master)](https://travis-ci.org/snieking/ansible-role-keystore-truststore)

An Ansible Role for creating a keystore and truststore with self-signed certificates.

Requirements
------------

A Java installation with JAVA_HOME configured is required on the host.

OpenSSL is required on the host.

Pip is required on the host. See the example Playbook.

Role Variables
--------------

**ca_path: /tmp/testCA** \
**Default:** yes \
The directory where the Certificate Authority should exist.

**trusted_ca_path:** \
**Default:** no \
Path of trusted certificate authorities (certification files) that should be imported to the truststore.

**expiration_days: 365** \
**Default:** yes \
Expiration time in days of the certificates.

**common_name:** \
**Default:** no

**country:** \
**Default:** no

**state:** \
**Default:** no

**locality:** \
**Default:** no

**organization:** \
**Default:** no

**organizational_unit:** \
**Default:** no

**keystore_name: keystore** \
**Default:** yes

**truststore_name: truststore** \
**Default:** yes

**clean_up:** \
**Default:** yes \
If a clean up should be made before running. When a clean up occurrs, all the old certificates and keystores are removed.

Example Playbook
----------------

The following playbook creates and signs certificates with our provided configuration. CN, C, ST, L, O & ON should be set to whatever you want. In the services we can configure which services and alternative names that the certificates should work for.
```yaml
- hosts: localhost
  connection: local
  vars_prompt:
    - name: "keystore_password"
      prompt: "Please provide a password for the keystore"
  pre_tasks:
    - name: ensure pip is installed
      easy_install: { name: pip, state: latest }
      become: yes
  roles:
    - role: snieking.keystore_truststore
      trusted_ca_path: /my/trusted/ca-path/
      clean_up: no
      common_name: thecuriousdev.org
      country: SE
      state: Stockholm Country
      locality: Stockholm
      organization: thecuriousdev
      organizational_unit: blog
      alt_names:
        - "DNS.1  = testservice"
        - "DNS.2  = localhost"
        - "IP.1   = 127.0.0.1"
```

License
-------

BSD, MIT

Author Information
------------------

Viktor Plane [https://thecuriousdev.org](https://thecuriousdev.org)
