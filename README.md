# docker-engine-vagrant
Vagrant files to automate the setup of docker engine.

**Instructions to use this vagrant setup**

Install Oracle VirtualBox
Install Vagrant
In a terminal run: 
    vagrant plugin install vagrant-hostmanager
    git clone git@github.com:anokun7/docker-engine-vagrant.git ~/docker-engine-vagrant
Download the file docker-cs-engine-rpm.sh from https://hub.docker.com/account/licenses/ [You will have to register for a hub account]
Place the file docker-cs-engine-rpm.sh under ~/docker-engine-vagrant
In a terminal run:
    cd ~/docker-engine-vagrant
    vagrant up
(You may be asked to provide your host machine's password, this is used to update /etc/hosts file)
    vagrant ssh

