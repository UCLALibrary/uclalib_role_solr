# UCLALib Ansible Role: Solr

Deploys Apache Solr 7 on RHEL servers

## Dependencies

* uclalib_role_java
* uclalib_role_apache
* uclalib_role_iptables

This role is capable of deploying Solr in the following configurations:

* Standalone: a single Solr instance

## Variables

solr_version - defines the version of Solr to use (e.g. 4.2.0, etc.)

solr_url - defines the URL to download Solr

solr_user - defines the user to own Solr files and run the Solr process

solr_service_name - defines the name of the Solr process

solr_install_dir - defines the top-level directory where Solr will be installed

solr_base_dir - defines the full path where Solr is installed

solr_data_dir - defines the full path where the Solr indexes/cores will reside

solr_port - defines the network port the Solr process will bind to

solr_config_file - defines the path to the Solr installation configuration file

solr_java_min_mem - defines the Solr process minimum memory allocation

solr_java_max_mem - defines the Solr process maximum memory allocation

solr_cores - the dictionary list of all Solr cores to be used in this instance
  * ident - defines the names of the cores to configure within this Solr instance
  * type - defines the external application using the solr core (e.g. default, drupal, etc).
    * the `type` variable is used in conjunction with application specific solr configuration files. You will need to manually put the appropriate files in the `files` directory for this role.
      * the naming convention for solr configuration files is: `appname_solr-conf`

## Sample Variable Definition Formats

#### Standalone Solr Instance
```
solr_cores:
  - ident: core1
    type: default
  - ident: core2
    type: drupal
  - ident: core3
    type: hyrax
```

The variable definitions should be placed in the playbook under the `vars` statement.
Example:
```
---
- name: uclalib_solr.yml
  sudo: true
  hosts: test
  vars:
    iptables_allowed_input_rules:
      - src_ip: 164.67.0.0/16
        dest_port: 80
        protocol: tcp
    solr_cores:
      - ident: core1
        type: default
      - ident: core2
        type: drupal
      - ident: core3
        type: hyrax

    roles:
      - { role: uclalib_role_java }
      - { role: uclalib_role_apache }
      - { role: uclalib_role_solr }
      - { role: uclalib_role_iptables }
```
