# docker-engine-vagrant
Vagrant files to automate the setup of docker engine.

**Instructions to use this vagrant setup**

1. Install Oracle VirtualBox
2. Install Vagrant
3. In a terminal run: 
```
vagrant plugin install vagrant-hostmanager
git clone git@github.com:anokun7/docker-engine-vagrant.git ~/docker-engine-vagrant
```
4. Download the file docker-cs-engine-rpm.sh from `https://hub.docker.com/account/licenses/` [You will have to register for a hub account]
5. Place the file docker-cs-engine-rpm.sh under ~/docker-engine-vagrant
6. In a terminal run:
```
cd ~/docker-engine-vagrant
vagrant up   
```
_You may be asked to provide your host machine's password, this is used to update /etc/hosts file_
```
vagrant ssh
```
