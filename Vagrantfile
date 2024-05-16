# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # setup control node
  config.vm.define "controller" do |control|
    control.vm.box = "bento/ubuntu-24.04"
    control.vm.box_version = "202404.26.0"
    config.vm.network "private_network", type: "dhcp"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 1
    end
    
    controller.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook_controller.yml"
    end
  end
  
  # setup n_workers number of worker nodes
  n_workers = 2
  (1..n_workers).each do |i|
    config.vm.define "node#{i}" do |worker|
      worker.vm.box = "bento/ubuntu-24.04"
      worker.vm.box_version = "202404.26.0"
      worker.vm.network "private_network", type: "dhcp"

      worker.vm.provider "virtualbox" do |vb|
        vb.memory = 6144
        vb.cpus = 2
      end
    end

    config.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook_node.yml"
    end
  end
end
