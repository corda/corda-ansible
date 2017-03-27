# corda-ansible

## Description
This role provides a minimal set of steps require to install Corda on a Linux machine (currently tested only with Ubuntu) along with all necessary templates and an example inventory file ( in the *hosts* file).

## Simple Usage

- For a sensible scenario install at least 3 Ubuntu 16.04 virtual or physical servers.
- Modify the **hosts** file and fill it with valid information about *city* (just for location on a node on network map), *legal node name* (for *network map*), *email address* and node *role*. These information are going to be use by Ansible to create a valid *node.conf* file.
- run **ansible-playbook -i hosts corda.yml**

## Task for Corda installation

- Install necessary packages (Java with JavaFX, NTP)
- Create an user and a directory for Corda
- Create the systemd configuration for Corda node and webserver
- Prepare Corda configuration file (*node.conf*)
- Install Corda jars (node and webserver) either from Maven Central, or from your local machine.


##Limitations
- works on Ubuntu only
- uses OpenJDK. It's going to use with Oracle Java with it's installed and configured as default Java
