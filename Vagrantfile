# -*- mode: ruby -*-
# vi: set ft=ruby :

# Define the number of worker nodes
n_workers = 2

# Run script to create inventory file
File.open("inventory.ini", "w") do |file|
  file.write("[controllers]\n")
  file.write("controller ansible_host=192.168.56.10\n")
  file.write("\n")
  file.write("[workers]\n")
  (1..n_workers).each do |i|
    file.write("node#{i} ansible_host=192.168.56.#{i+10}\n")
  end
end

Vagrant.configure("2") do |config|
  # setup control node
  config.vm.define "controller" do |control|
    control.vm.box = "bento/ubuntu-24.04"
    control.vm.box_version = "202404.26.0"
    control.vm.hostname = "controller"
    config.vm.network "private_network", ip: "192.168.56.10"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 1
    end
    
    control.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.inventory_path = "inventory.ini"
      ansible.playbook = "playbook_controller.yml"
    end
  end
  
  # setup n_workers number of worker nodes
  (1..n_workers).each do |i|
    config.vm.define "node#{i}" do |worker|
      worker.vm.box = "bento/ubuntu-24.04"
      worker.vm.box_version = "202404.26.0"
      worker.vm.hostname = "node#{i}"
      worker.vm.network "private_network", ip: "192.168.56.#{i+10}"

      worker.vm.provider "virtualbox" do |vb|
        vb.memory = 6144
        vb.cpus = 2
      end

      worker.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.inventory_path = "inventory.ini"
        ansible.playbook = "playbook_node.yml"
      end
    end
  end
end
