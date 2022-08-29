# -*- mode: ruby -*# vi: set ft=ruby :
require 'yaml'
vagrantConfig = YAML.load_file 'Vagrantfile.config.yml'
Vagrant.configure("2") do |config|
    config.vm.box = "generic/rocky8"

    config.vm.define "application" do |application|
        application.vm.network "private_network", ip: vagrantConfig['ip']
        application.vm.hostname = "application"
    end

    config.vm.synced_folder "projects/", "/home/vagrant/projects", owner:"vagrant", group: "vagrant"

    config.vm.provider "libvirt" do |vb|
      vb.cpus = 2
	    vb.memory = "4096"
    end

    config.vm.provision "shell", inline: "sudo dnf update -y"
    config.vm.provision "shell", inline: "sudo dnf upgrade -y"
  	config.vm.provision "shell", inline: "sudo dnf groupinstall \"Development tools\" -y"
end
