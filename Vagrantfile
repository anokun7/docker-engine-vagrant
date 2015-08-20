Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/centos71"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update -y && sudo yum upgrade -y
    chmod 755 /vagrant/docker-cs-engine-rpm.sh
    sudo /vagrant/docker-cs-engine-rpm.sh
    sudo yum install docker-engine-cs -y
    sudo systemctl enable docker.service
    sudo systemctl start docker.service
    sudo usermod -a -G docker vagrant
  SHELL
end
