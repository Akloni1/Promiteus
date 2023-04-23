# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

   #node1
  config.vm.define "node1" do |node1|
    node1.vm.box = "ubuntu/jammy64"
    node1.vm.hostname = "node1"
    node1.vm.network "private_network", ip: "192.168.99.101"
    node1.vm.network "forwarded_port", guest: 9090, host: 9090
    node1.vm.provision "shell", path: "add_hosts.sh"

    node1.vm.provider "virtualbox" do |v|
      v.gui = false
      v.memory = 4096
      v.cpus = 2
    end
  end

  #node2 
  config.vm.define "node2" do |node2|
    node2.vm.box = "ubuntu/jammy64"
    node2.vm.hostname = "node2"
    node2.vm.network "private_network", ip: "192.168.99.102"
    node2.vm.network "forwarded_port", guest: 9100, host: 9100
    node2.vm.provision "shell", path: "add_hosts.sh"
    node2.vm.provider "virtualbox" do |v|
      v.gui = false
      v.memory = 2048
      v.cpus = 2
    end
	node2.vm.provision :docker
      node2.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run: "always"
  end
  
end
