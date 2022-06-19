# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "sektor"
  config.vm.define "sektor"
  config.vagrant.plugins = ['vagrant-vbguest']
  config.vm.network "private_network", ip: "192.168.33.23"
  config.vm.synced_folder "./", "/home/vagrant/project"

  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = "2048"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install curl git cmake vim -y
  SHELL

  config.vm.provision "docker" do |d|
    d.run "nginx", image: "nginx:stable",
      args: "-p 8080:80"
  end

  # Ansible provisioner
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/playbook.yml"
    ansible.inventory_path = "ansible/inventory"
    ansible.become = true
  end

end
