*******
Delegated driver installation guide
*******

Requirements
============

Machines are pre-provisioned and externally managed via vagrant. Boxes are taken from https://roboxes.org/

Install
=======

* install vagrant
* vagrant boxes
    ```shell
    vagrant box add generic/alma8
    vagrant box add generic/centos7
    vagrant box add generic/centos8
    vagrant box add generic/fedora28
    vagrant box add generic/fedora29
    vagrant box add generic/fedora35
    vagrant box add generic/opensuse15
    vagrant box add generic/rhel7
    vagrant box add generic/rhel8
    ```
* create vagrant environment
    ```shell
    vagrant up
    ```
* export ssh config
    ```shell
    vagrant ssh-config > molecule/physical/ssh_config
    ```
* copy and change permissions on identityfiles.
    ```shell
    VAGRANTFILE_BASEDIR=/mnt/c/Users/Public/Documents/EL
    pushd molecule/physical/.ssh
    for file in $(ls -1 "${VAGRANTFILE_BASEDIR}/.vagrant/machines/"*"/"*"/private_key")
    do
    cp -v "$file" "$(basename $(dirname $(dirname $file)))"
    chmod 0600 "$(basename $(dirname $(dirname $file)))"
    done
    ```
* edit the path of IdentityFile property in ssh_config

Access hosts
------------

ssh to all hosts:

    for host in $(\grep -Po '^Host\s+\K.*'  molecule/physical/ssh_config); do echo $host ; ssh -X -F molecule/physical/ssh_config $host ; done


Details 
-------

vagrant providers
~~~~~~~~~~~~~~~~

* hyper-v

this is on windows desktop with hyper-v virtualization and ansible running inside WSL.
forwarding needs to be setup between the different switches:

    Get-NetIPInterface | where {$_.InterfaceAlias -eq 'vEthernet (WSL)' -or $_.InterfaceAlias -eq 'vEthernet (Default Switch)'} | Set-NetIPInterface -Forwarding Enabled

vagrant image
~~~~~~~~~~~~~

* generic/opensuse15

this image has some updating issues. it maybe required to login once and run: `sudo zypper ref && sudo zypper up && sudo reboot`
