# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Configura la máquina virtual del servidor DHCP (Ubuntu Trusty64)
  config.vm.define "server" do |server|
    server.vm.box = "debian/bookworm64" 
    server.vm.network "private_network", ip: "192.168.56.10"
    server.vm.network "private_network", ip: "192.168.57.10", virtualbox__intnet: true
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
    server.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y isc-dhcp-server
    SHELL
  end

  # Configura dos clientes DHCP con Debian Bookworm64
  config.vm.define "c1" do |c1|
    c1.vm.box = "debian/bookworm64" 
    c1.vm.network "private_network", type: "dhcp", virtualbox__intnet:true
    c1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
  end

  config.vm.define "c2" do |c2|
    c2.vm.box = "debian/bookworm64" 
    c2.vm.network "private_network", type: "dhcp",
    mac: "5CA1AB1E0001",
    virtualbox__intnet: true
    c2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
  end
end
