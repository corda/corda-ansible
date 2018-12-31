# corda-ansible

## Description
This role provides a minimal set of steps required to install Corda on a Linux machine (currently tested with Ubuntu and CentOS) along with all necessary templates (Corda node.conf and systemD script).

## Corda installation tasks carried by Ansible

This is a summary of the actions performed by Ansible:

- Install necessary packages (including OpenJDK from zulu.org by default)
- Create a user and a directory for Corda
- Create the systemd configuration for Corda node
- Prepare Corda configuration file (*node.conf*)
- Install Corda jar (node) either from Maven Central, from your local machine (e.g. to use with Corda Enterprise) or snapshot from R3 artifactory
- Optional node can be register with Doorman

## Role Variables

All variables are defined in *defaults/main.yml*. Some of them should be changed from the default value.

|  variable | default value | usage |
| --- | --- | --- |
| corda_admin_email | "corda@example.com" | contact email address sent to Zone Operator |
| corda_devmode | "true" | define if node is in 'development mode' (see notes) |
| corda_dir_location | /opt/corda | directory where Corda is going to be installed |
| corda_host_p2p | "{{ ansible_hostname }}" | address node exported to Network Map |
| corda_host_rpc | 0.0.0.0 | local address rpc binds to |
| corda_initial_registration | false | define if register node with Doorman (see notes) |
| corda_java | openjdk | What java to use (see notes) |
| corda_java_options | -Xmx2048 | extra parameters for Java |
| corda_local_path | "" | path to local files you might copy over (see notes) |
| corda_name_city | London | part of Legal Name in node.conf |
| corda_name_country | GB | part of Legal Name in node.conf |
| corda_name_org | Corda | part of Legal Name in node.conf |
| corda_name_org_unit | Corda | (not in use) can be part of Legal Name in node.conf |
| corda_notary_type | "non_validating" | type of notary (see notes) |
| corda_password_keystore |  | value for node keystore, should be in encrypted with Ansible Vault |
| corda_password_truststore | password | password for truststore shared by Zone operator |
| corda_port_p2p | 10002 | port for P2P connections |
| corda_port_rpc | 10003 | port RPC binds to |
| corda_port_rpc_admin | 10004 | port RPC binds to for Admin connections |
| corda_port_h2 | 11000 | port for local H2 DB |
| corda_role | node | what role should have corda.jar |
| corda_rpc | disable | define if RPC should be enabled (see notes)|
| corda_rpc_user | corda | user for RPC connection |
| corda_rpc_password | corda_is_awesome | password for RPC user |
| corda_source | maven | source of corda.jar (see notes) |
| corda_url_doorman | "http://example-change.it" | URL for Zone Doorman (not for devmode) |
| corda_url_networkmap | "http://example-change.it" | URL for Zone Network Map (not for devmode ) |
| corda_user | corda | name for UNIX user dedicated to run corda |
| corda_version | 3.3 | version of corda to install |

### Notes ###

- *corda_devmode* is a string not a boolean, so to change set it with: **corda_devmode: !!str false**
- if *corda_initial_registration* is set to'true' extra step registring node Doorman defined in corda_url_doorman is going to be performed. This is not for devmode
- setting *corda_java* to a value other than openjdk will prevent the role from installing OpenJDK from zulu.org (no Java VM will be installed)
- *corda_local_path* can be use to point where files e.g. corda.jar or network-root-truststore.jks are located on local machine. It can be ignore for most cases (other than initial registration or using 'local' as a source)
- *corda_notary_type* can be either **validating** or **non_validating**
- *corda_role* has to be be either **node** or **notary**
- *corda_rpc* is a string and should be **enabled** or **disable**
- *corda_source* can be 'local' (e.g. when you would like to use this role with Corda Enteprise, or you own Corda build), 'maven' for official builds or 'artifactory' to download daily snapshot. If you are not sure which version to download please visit [Maven Central](http://repo1.maven.org/maven2/net/corda/corda/).


## Old Example (working with old NetworkMap - version up to 2)

- For a sensible scenario install at least 3 Ubuntu 16.04 or CentOS 7 virtual or physical servers. There is a Vagrant example  with 3 Ubuntu nodes attached to this repository in (examples/vagrant/ubuntu3nodes).
- Modify the **hosts** file and fill it with valid information about *city* (just for location on a node on network map), *legal node name* (for *network map*), *email address* and node *role*. This information is going to be used by Ansible to create a valid *node.conf* file.
- run `ansible-playbook -i hosts corda.yml`

## Limitations

- tested with Ubuntu LTS (16.04/18.04) CentOS 7
- installs OpenJDK from zulu.org. However, Corda will use your machine's default Java VM. Therefore, if you installed Oracle JDK (e.g. using [ansiblebit/oracle-java](https://github.com/ansiblebit/oracle-java) role) and set it up as the default Java VM, Corda will use it.
