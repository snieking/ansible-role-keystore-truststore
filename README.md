Ansible Role: Keystore Truststore
=========
[![Build Status](https://travis-ci.org/snieking/ansible-role-keystore-truststore.svg?branch=master)](https://travis-ci.org/snieking/ansible-role-keystore-truststore)

An Ansible Role for creating a keystore and truststore with self-signed certificates.

Requirements
------------

A Java installation with JAVA_HOME configured is required on the host.

OpenSSL is required on the host.

Pip is required on the host as well as the python package pexists that can be installed with pip. See the example Playbook.

Role Variables
--------------

**ca_path: /tmp/testCA** \
**Default:** yes \
The directory where the Certificate Authority should exist.

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

**services:** \
**Default:** no \
List of services. Each service has a name, and a list of alternative names. See playbook example below.

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
    - name: ensure pexists is installed
      pip: { name: pexpect, state: present }
  roles:
    - role: snieking.keystore_truststore
      common_name: thecuriousdev.org
      country: SE
      state: Stockholm
      locality: Grondal
      organization: thecuriousdev
      organizational_unit: blog
      services:
        - name: testservice
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
