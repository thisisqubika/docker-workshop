# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  # config.vm.box_check_update = false

  config.vm.network "forwarded_port", guest: 8080, host: 80
  config.vm.network "forwarded_port", guest: 8081, host: 8080

  config.vm.define "dkrworkshop"
  config.vm.hostname = "dkrworkshop"

  config.vm.provider "virtualbox" do |vb|
     vb.name = "dkrworkshop"
  end
  
  config.vm.provision "docker",
     images: ["hello-world"]
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     DEBIAN_FRONTEND=noninteractive apt-get install -y docker-compose bridge-utils
     apt-get clean
  SHELL
end
