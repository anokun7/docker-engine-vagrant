Vagrant.configure(2) do |config|

  config.vm.define 'centos' do |centos|
    centos.vm.box = "boxcutter/centos71"
    centos.vm.hostname = 'centos71.docker.demo'
    centos.vm.network "private_network", ip: "10.20.1.2"
    centos.vm.network "forwarded_port", guest: 80, host: 8080
    centos.vm.network "forwarded_port", guest: 443, host: 8443

   # Enable provisioning with a shell script 
    centos.vm.provision "shell", inline: <<-SHELLC
      chmod 755 /vagrant/docker-cs-engine-rpm.sh
      sudo /vagrant/docker-cs-engine-rpm.sh
      sudo yum install docker-engine-cs telnet nc lynx -y
      sudo systemctl enable docker.service
      sudo systemctl start docker.service
      sudo usermod -a -G docker vagrant

    # Install docker-compose
      sudo curl -L https://github.com/docker/compose/releases/download/1.3.3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose

    # Install DTR
    sudo bash -c "$(sudo docker run docker/trusted-registry install)"

    SHELLC
  end

  config.vm.define 'ubuntu' do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.hostname = 'ubuntu14.docker.demo'
    ubuntu.vm.synced_folder ".", "/vagrant"
    ubuntu.vm.network "private_network", ip: "10.20.1.3"
    ubuntu.vm.network "forwarded_port", guest: 80, host: 9080
    ubuntu.vm.network "forwarded_port", guest: 443, host: 2443

   # Enable provisioning with a shell script 
    ubuntu.vm.provision "shell", inline: <<-SHELLU
      sudo apt-get install -y linux-image-extra-virtual dkms build-essential linux-headers-generic virtualbox-guest-x11

      mkdir -p /mnt/virtualbox
      mount -o loop /home/vagrant/VBoxGuest*.iso /mnt/virtualbox
      sh /mnt/virtualbox/VBoxLinuxAdditions.run
      ln -s /opt/VBoxGuestAdditions-*/lib/VBoxGuestAdditions /usr/lib/VBoxGuestAdditions
      umount /mnt/virtualbox
      rm -rf /home/vagrant/VBoxGuest*.iso

      chmod 755 /vagrant/docker-cs-engine-deb.sh
      sudo /vagrant/docker-cs-engine-deb.sh
      sudo apt-get install docker-engine-cs
      sudo service docker restart
      sudo usermod -a -G docker vagrant

    # Install docker-compose
      sudo curl -L https://github.com/docker/compose/releases/download/1.3.3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose

    # Install DTR
    sudo bash -c "$(sudo docker run docker/trusted-registry install)"

    # Needs a reboot
      sudo reboot

    SHELLU
  end
end
