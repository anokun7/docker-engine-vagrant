Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/centos71"
  config.vm.hostname = 'engine.docker.demo'
  config.vm.network "private_network", ip: "10.20.1.0"
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update && sudo yum upgrade -y
    chmod 755 /vagrant/docker-cs-engine-rpm.sh
    sudo /vagrant/docker-cs-engine-rpm.sh
    sudo yum install docker-engine-cs -y
    sudo systemctl enable docker.service
    sudo systemctl start docker.service
    sudo usermod -a -G docker vagrant
  SHELL
end
