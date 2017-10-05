# corda-ansible

## Description
This role provides a minimal set of steps required to install Corda on a Linux machine (currently tested only with Ubuntu and CentOS) along with all necessary templates and an example inventory file (in the *hosts* file).

## Simple Usage

- For a sensible scenario install at least 3 Ubuntu 16.04 or CentOS 7 virtual or physical servers. There is a Vagrant example  with 3 Ubuntu nodes attached to this repository in (examples/vagrant/ubuntu3nodes).
- Modify the **hosts** file and fill it with valid information about *city* (just for location on a node on network map), *legal node name* (for *network map*), *email address* and node *role*. This information is going to be used by Ansible to create a valid *node.conf* file.
- run `ansible-playbook -i hosts corda.yml`

## Role Variables

All variables are defined in *defaults/main.yml*. Many of them shouldn't been leave with default value.

|  variable | default value |
| --- | --- |
| corda_user | corda |
| corda_dir_location | /opt/corda |
| corda_host_p2p | "{{ ansible_hostname }}" |
| corda_host_rpc | "{{ ansible_hostname }}" |
| corda_port_p2p | 10002 |
| corda_port_rpc | 10003 |
| corda_port_web | 10004 |
| corda_port_h2 | 11000 |
| corda_portal_user | corda |
| corda_portal_password | corda_is_awesome |
| corda_devmode | "true" |
| corda_java | openjdk |
| corda_java_options | -Xmx2048 |
| corda_version | 1.0.0 |
| corda_source | maven |
| corda_local_path | "" |
| corda_country | GB |
| corda_city | London |
| corda_org | Corda |
| corda_org_unit | Corda |
| corda_admin_email | "change_it@corda.net" |
| corda_role | node |
| corda_notary_type | "non_validating" |
| corda_networkmap_address | "example-change.it" |
| corda_networkmap_name | "O=Corda, L=London, C=GB" |
| corda_doorman_url | "example-change.it" |
| corda_legal_name | (_deprecated in 1.0_) "Corda Test Node - Change it" |

Please note: 
- If you are not sure what version to use please visit [Maven Central](http://repo1.maven.org/maven2/net/corda/corda/).
- *corda_devmode* is a string not a boolen.
- *corda_role* has to be be one of 3 (**node**, **notary**, **networkmap**)
- *corda_notary_type* can be ethier **validating** or **non_validating**
- setting *corda_java* to a value diffrent than openjdk will stop role ot install OpenJDK from zulu.org (no Java VM will be install)


## Corda installation tasks carried by Ansible

This is a summary of the actions performed by Ansible.

- Install necessary packages (including OpenJDK from zulu.org by default)
- Create a user and a directory for Corda
- Create the systemd configuration for Corda node and webserver
- Prepare Corda configuration file (*node.conf*)
- Install Corda jars (node and webserver) either from Maven Central, or from your local machine.


## Limitations

- tested with Ubuntu 16.04 only CentOS 7 (7.3) only
- install only OpenJDK from zulu.org (on request). However, Corda is going to use a default Java VM. Therefore, if you installed Oracle JDK (e.g. using [ansiblebit/oracle-java](https://github.com/ansiblebit/oracle-java) role) and set it up as the default Java VM, Corda is going to it.
