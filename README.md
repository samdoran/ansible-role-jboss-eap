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
| `jboss_eap_install_method` | `rpm` | How it install EAP: `rpm` or `zip`. Zip installation isn't currently built. |
| `jboss_eap_base_version` | `6.4` | Base EAP version to install. Can be a major version (6 or 7) or a minor version (6.4 or 7.0) |
| `jboss_eap_service_name` | `jbossas` or `eap7-standalone` | Sets the service name based on the EAP version. |
| `jboss_eap_runtime_conf_file` | `{{ jboss_eap_jboss_home }}/bin/{{ jboss_eap_configuration }}.conf` | Runtime configuration file location. |
| `jboss_eap_service_conf_dir` | `[varies by OS version]` |  |
| `jboss_eap_service_conf_file` | `[varies by OS version]` |  |
| `jboss_eap_admin_user` | `jbadmin` | Default admin account created after installation. |
| `jboss_eap_admin_password` | `JBadmin-581` | Password for default admin account. |

Service configuration for EAP6 (`/etc/sysconfig/jbossas`)

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_user` | `jboss` | Username that owns the JBoss process |
| `jboss_eap_group` | `jboss` | Group that owns the JBoss process |
| `jboss_eap_startup_wait` | `60` | The amount of time to wait for startup |
| `jboss_eap_shutdown_wait` | `20` | The amount of time to wait for shutdown |
| `jboss_eap_jboss_home` | `/usr/share/{{ jboss_eap_service_name }}` | Where JBoss is located. |
| `jboss_eap_configuration` | `standalone` | JBoss configuration to starte |
| `jboss_eap_console_log` | `/var/log/jbossas/$JBossCONF/console.log` | Locatin of the console log. |
| `jboss_eap_sh` | `$JBoss_HOME/bin/$JBossCONF.sh` | Script that starts JBoss. |
| `jboss_eap_server_config` | `{{ jboss_eap_configuration }}.xml` | Server configuration to start. |
| `jboss_eap_module_path` | `$JBOSS_HOME/modules` | JBoss module directory. |

Service settings for EAP7 (`/etc/opt/rh/eap7/wildfly/eap7-standalone`)

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_wildfly_console_log` | `/var/opt/rh/eap7/log/wildfly/standalone/console.log` | Location to keep the console log |
| `jboss_eap_wildfly_sh` | `/opt/rh/eap7/root/usr/share/wildfly/bin/standalone.sh` | Define the script to use to start wildfly |
| `jboss_eap_wildfly_module_path` | `/opt/rh/eap7/root/usr/share/wildfly/modules` | Define where wildfly module directory is |
| `jboss_eap_wildfly_bind` | `0.0.0.0` | The address to bind to |

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
