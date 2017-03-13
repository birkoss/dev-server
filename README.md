Create a new Virtual Machine
============================

* Create a new VM running Ubuntu Server

* Setup the first adapter as a *NAT*, and the second as a *Host-only* adapter running on 192.168.10.*.

* In the VirtualBox settings, add a shared folder named Docker while selecting Auto-Mount

* In the file /etc/network/interfaces, configure the second adapter :

	auto enp0s8
	iface enp0s8 inet static
		address 192.168.10.101
		network 192.168.10.0
		netmask 255.255.255.0
		broadcast 192.168.10.25


On the VM server
================

Configure the host to access the shared folder
----------------------------------------------

* Install the necessary package for mounting and installing the VirtualBox Guest Addition CD: **apt-get install build-essential linux-headers-`uname -r` dkms**

* Mount the VirtualBox Guest Addition CD from VirtualBox

* Mount the CD in Ubuntu using : **mount /dev/cdrom /media/cdrom/**

* Install the Guest Addition CD : **sudo /media/cdrom/VBoxLinuxAdditions.run**

* Add your user to the group vboxsf : **sudo usermod -a -G vboxsf USERNAME**

* The folder /media/sf_Docker should be available after a reboot.

Installing Docker
-----------------

* Install those packages (probably have already it) : **sudo apt-get install apt-transport-https ca-certificates curl software-properties-common**

* Install Docker's official GPG Key: **curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -**

* Add the Docker's repository : **sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"**

* Update the packages list : **sudo apt-get update**

* Installing Docker : **sudo apt-get install docker-ce**

Installing Docker Compose
-------------------------

Downloading docker-compose: **curl -L "https://github.com/docker/compose/releases/download/1.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose**

Make it runnable : **sudo chmod +x /usr/local/bin/docker-compose**
