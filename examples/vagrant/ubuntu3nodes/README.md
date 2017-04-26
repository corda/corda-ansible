# Vagrant 3 nodes Corda Network

## Description
This is a multinode Vagrantfile for a 3 nodes Corda network. The configuration is done by Ansible role.

## Prerequisites
- Vagrant  ([Installation instruction](https://www.vagrantup.com/docs/installation/))
- VirtalBox (for VMs, can be replace by other provider) ([Documentation](https://www.virtualbox.org/wiki/VirtualBox))
- Ansible (of course) ([Installation instruction](http://docs.ansible.com/ansible/intro_installation.html))
- this role installed on your machine

## VM Spec
This example uses Ubuntu 16.04 LTS VirtualBox VMs with 3GB memory, around 2GB of disk space and 1 virtual CPU.

## Usage
- Copy Vagrantfile and corda.yml files into desire location
- check content of the **corda.yml** (especially _version_ and _source_ variables)
- check configuration in **Vagrantfile** (e.g. provider, number of CPUs and memory as well as Corda node specific informations)
- run **vagrant up** to start the network. It might take some time

After that you can access vagrant control machine in the Vagrant standard way. The easiest way to reach VM shell is with **vagrant ssh node<number>** (where <number> is 1 to 3).
For more information about multinode Vagrant look at this [documentation](https://www.vagrantup.com/docs/multi-machine/).

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

