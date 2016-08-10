JBoss Enterprise Application Platform
=========
[![Galaxy](https://img.shields.io/badge/galaxy-samdoran.jboss--eap-blue.svg?style=flat)](https://galaxy.ansible.com/samdoran/jboss-eap)

Install Red Hat JBoss Enterprise Application Platform.

Requirements
------------

Red Hat subscription.

Role Variables
--------------

Variables are defined in `defaults/main.yml` as well as `vars/`. Based on the operating system family, version, and installation method, variables will be set the appropriate values.

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_install_method` | `rpm` | How it install EAP: `rpm` or `zip`. |
| `jboss_eap_zip_file_url` | `[undefined]` |  When defined, download the EAP zip file from here instead of copying from the control node. If this is undefined, the zip file must be placed in the `files` directory within the role and named `{{ jboss_eap_zip_file_name }}` |
| `jboss_eap_patch_file_url` | `[undefined]` |  When defined, download the EAP patch file from here instead of copying from the control node. If this is undefined, the patch file must be placed in the `files` directory within the role and named `{{ jboss_eap_patch_file_name }}` |
| `jboss_eap_patch` | `yes` | Whether or not to apply EAP patch |
| `jboss_eap_base_version` | `6.4` | Base EAP version to install. Can be a major version (6 or 7) or a minor version (6.4 or 7.0) |
| `jboss_eap_minor_version` | `8` | Minor version, e.g., 6.4.8. |
| `jboss_eap_runtime_conf_file` | `{{ jboss_eap_jboss_home }}/bin/{{ jboss_eap_configuration }}.conf` | Runtime configuration file location. |
| `jboss_eap_java_home` | `/usr/lib/jvm/jre` | Path to `java` executable. Use `/usr/lib/jvm/jre` for JRE, `/usr/lib/jvm/jdk` for JDK. |
| `jboss_eap_javapth` | `$JAVA_HOME/bin` | Appended to `PATH`. |
| `jboss_eap_admin_user` | `jbadmin` | Default admin account created after installation. |
| `jboss_eap_admin_password` | `JBadmin-581` | Password for default admin account. |

Variables related to Kerberos and keytab files.

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_configure_kerberos` | `no` | Whether or not to run tasks in kerberos.yml |
| `jboss_eap_keytab_file_dir` | `[undefined]` | Directory containing keytab files on the control server if they are not stored in the `files` directory within the role. Since these are sensitive, it is recommended to store them outside of the role so they do not get committed to version control. |
| `jboss_eap_keytab_dir` | `/etc/jboss/keytab` | Directory where keytab files will be stored on the managed system. |
| `jboss_eap_keytab_filename` | `keytab` | Filename of keytab. |

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
| `jboss_eap_server_config_script` | `[undefined]` | When defined, copy this script to the remote server and run it rather than managing the entire `standalone.xml`. |
| `jboss_eap_module_path` | `$JBOSS_HOME/modules` | JBoss module directory. |

Service settings for EAP7 (`/etc/opt/rh/eap7/wildfly/eap7-standalone`)

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_wildfly_console_log` | `/var/opt/rh/eap7/log/wildfly/standalone/console.log` | Location to keep the console log |
| `jboss_eap_wildfly_sh` | `/opt/rh/eap7/root/usr/share/wildfly/bin/standalone.sh` | Define the script to use to start wildfly |
| `jboss_eap_wildfly_module_path` | `/opt/rh/eap7/root/usr/share/wildfly/modules` | Define where wildfly module directory is |
| `jboss_eap_wildfly_bind` | `0.0.0.0` | The address to bind to |

Runtime settings for EAP6

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `jboss_eap_runtime_bind_address` | `0.0.0.0` | Address EAP will bind to. |
| `jboss_eap_bind_address_management` | `0.0.0.0` | Address EAP management will bind to. |
| `jboss_eap_runtime_logging_timezone` | `America/New_York` | Timezone. |
| `jboss_eap_runtime_initial_memory` | `{{ ansible_memtotal_mb // 4 }}m` | Xms used in java options. |
| `jboss_eap_runtime_max_memory` | `{{ ansible_memtotal_mb // 2 }}m` | Xmx used in java options. |
| `jboss_eap_runtime_maxpermsize` | `{{ ansible_memtotal_mb // 8 }}m` | MaxPermSize used in java options. |
| `jboss_eap_runtime_max_fd` | `maximum` | Specify the maximum file descriptor limit, use "max" or "maximum" to use |
| `jboss_eap_runtime_profiler` | `null` | Specify the profiler configuration file to load. Default is to not load profiler configuration file. |
| `jboss_eap_runtime_java_home` | `null` | Specify the location of the Java home directory. |
| `jboss_eap_runtime_java_bin` | `null` | Specify the exact Java VM executable to use. |
| `jboss_eap_runtime_preserve_java_opts` | `null` | Prevent manipulation of JVM options by shell scripts. true or false |
| `jboss_eap_runtime_java_opts` | `[see defaults/main.yml` | List of java options passed to EAP in the `standolne.conf` file. |

Dependencies
------------

- `samdoran.java`
- `samdoran.redhat-subscription`
- `samdoran.repo-epel`

Example Playbook
----------------

    - hosts: all
      roles:
         - samdoran.jboss-eap

License
-------

MIT
