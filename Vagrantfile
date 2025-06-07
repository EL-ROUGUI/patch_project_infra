# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  (1..3).each do |i|
    config.vm.define "server0#{i}" do |server|
      server.vm.box = "ubuntu/jammy64"
      server.vm.hostname = "server0#{i}"
      server.vm.network "private_network", ip: "192.168.56.1#{i}"

      server.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = "1"
      end
    end
  end
end