# Vagrant 3 nodes Corda Network

## Description
This is a multinode Vagrantfile for a 3 nodes Corda network. The configuration is done by Ansible role.

## Prerequisites
- Vagrant  [https://www.vagrantup.com/docs/installation/](Installation instruction)
- VirtalBox (for VMs, can be replace by other provider) [https://www.virtualbox.org/wiki/VirtualBox](Documentation)
- Ansible (of course) [http://docs.ansible.com/ansible/intro_installation.html](Installation instruction)
- this role installed on your machine

## VM Spec
This example uses Ubuntu 16.04 LTS VirtualBox VMs with 3GB memory and 1 virtual CPU.

## Usage
- Copy Vagrantfile and corda.yml files into desire location
- check content of the **corda.yml** (especially _version_ and _source_ variables)
- check configuration in **Vagrantfile** (e.g. provider, number of CPUs and memory)
- run **vagrant up** to start the network. It might take some time

### Example script for Unix

Please execute following commands from the directory this example is in.

```
roledir=$(cd $PWD/../../../; pwd)
destination="$HOME/Vagrant/Corda3Nodes"
mkdir -p $destination
cp Vagrantfile corda.yml $destination
cd $destination
ln -s $roledir $destination
vagrant up
```

