Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/centos71"
  config.vm.hostname = 'engine.docker.demo'
  config.vm.network "private_network", ip: "10.20.1.0"
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
# config.vm.network "forwarded_port", guest: 8080, host: 8080
# config.vm.network "forwarded_port", guest: 3306, host: 3306

# Enable provisioning with a shell script 
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update && sudo yum upgrade -y
    chmod 755 /vagrant/docker-cs-engine-rpm.sh
    sudo /vagrant/docker-cs-engine-rpm.sh
    sudo yum install docker-engine-cs -y
    sudo systemctl enable docker.service
    sudo systemctl start docker.service
    sudo usermod -a -G docker vagrant

# Install docker-compose
    sudo curl -L https://github.com/docker/compose/releases/download/1.3.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
  SHELL
end
