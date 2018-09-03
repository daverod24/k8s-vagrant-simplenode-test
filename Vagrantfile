# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.box_check_update = false
  config.vm.synced_folder "shared/", "/shared", create: true

  config.vm.define "k8s-ubuntu" do |server|
    server.vm.provider "virtualbox" do |vb|
	     vb.customize ["modifyvm", :id, "--cpus", "2"]
       vb.name = "k8s-ubuntu"
       vb.memory = 4096
    end
    server.vm.hostname = "k8s-ubuntu.local"
    server.vm.network "public_network",
        use_dhcp_assigned_default_route: true
    server.vm.network "private_network", ip: "10.0.0.120", :netmask => "255.255.0.0"
    server.vm.network "forwarded_port", guest: 80, host: 8080,
        auto_correct: true
    server.vm.provision "docker"    
    server.vm.provision :shell, :path => './provision-k8s', args: ENV['ARGS']
  end
end