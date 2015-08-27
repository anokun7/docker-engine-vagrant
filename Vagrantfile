Vagrant.configure(2) do |config|

  config.vm.define 'centos' do |centos|
    centos.vm.box = "boxcutter/centos71"
    centos.vm.hostname = 'centos71.docker.demo'
    centos.vm.network "private_network", ip: "10.20.1.0"

   # Not sure if I really need this.
   #centos.hostmanager.enabled = true
   #centos.hostmanager.manage_host = true

   # Enable provisioning with a shell script 
    centos.vm.provision "shell", inline: <<-SHELL
      sudo yum update -y && sudo yum upgrade -y
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
end
