# Vagrant 3 nodes Corda Network

## Description
This is a multinode Vagrantfile for a 3 nodes Corda network. The configuration is done by Ansible role.

## Prerequisites
- Vagrant  ([Installation instruction](https://www.vagrantup.com/docs/installation/))
- VirtalBox (for VMs, can be replace by other provider) ([Documentation](https://www.virtualbox.org/wiki/VirtualBox))
- Ansible (of course) ([Installation instruction](http://docs.ansible.com/ansible/intro_installation.html))
- this role installed on your machine

## Windows Limitation
It's very hard to make Vagrant and Ansible to work toghther on Windows. See [here](https://github.com/mitchellh/vagrant/issues/7731), [here](https://www.jeffgeerling.com/blog/2017/using-ubuntu-bash-windows-creators-update-vagrant) and [here](https://github.com/Microsoft/BashOnWindows/issues/733#issuecomment-266175270).
- One option is to run Vagrant without Ansible provisioning and then run Ansible separatly afterwords. To achive that you need to copy your SSH key on all Vagrant machines. See discussion on [StackOverflow](http://stackoverflow.com/questions/30075461/how-do-i-add-my-own-public-key-to-vagrant-vm) for suggestion how to do this.
- Another possibility is to install additional Ansible master VM. Can be very small.

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

