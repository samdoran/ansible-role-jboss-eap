JBoss Enterprise Application Platform
=========
[![Galaxy](https://img.shields.io/badge/galaxy-samdoran.jboss--eap-blue.svg?style=flat)](https://galaxy.ansible.com/samdoran/jboss-eap)

Install Red Hat JBoss Enterprise Application Platform.

Requirements
------------

Red Hat subscription.

Role Variables
--------------

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `` | `` |  |

Dependencies
------------

- `samdoran.java`
- `samdoran.redhat-subscription`
- `samdoran.repo-epel`

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - samdoran.jboss-eap

License
-------

MIT
