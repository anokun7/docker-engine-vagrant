Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/centos71"

  config.vm.define 'engine' do |engine|
    engine.vm.hostname = 'engine.docker.demo'
    engine.vm.network "private_network", ip: "10.20.1.0"
    engine.hostmanager.enabled = true
    engine.hostmanager.manage_host = true

    engine.vm.provision "shell", inline: <<-SHELL
      sudo yum update -y && sudo yum upgrade -y
      chmod 755 /vagrant/docker-cs-engine-rpm.sh
      sudo /vagrant/docker-cs-engine-rpm.sh
      sudo yum install docker-engine-cs -y
      sudo systemctl enable docker.service
      sudo systemctl start docker.service
      sudo usermod -a -G docker vagrant
    SHELL
  end
end
