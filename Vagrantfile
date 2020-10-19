# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  # config.vm.box_check_update = false

  config.vm.network "forwarded_port", host: 8000, guest: 80
  config.vm.network "forwarded_port", host: 8080, guest: 8080
  config.vm.network "forwarded_port", host: 8081, guest: 8081

  config.vm.define "dkrworkshop"
  config.vm.hostname = "dkrworkshop"

  config.vm.provider "virtualbox" do |vb|
     vb.name = "dkrworkshop"
  end
  
  config.vm.provision "docker",
     images: ["hello-world"]
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     DEBIAN_FRONTEND=noninteractive apt-get install -y docker-compose bridge-utils jq
     apt-get clean
  SHELL
end
