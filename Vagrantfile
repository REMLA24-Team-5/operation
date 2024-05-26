# -*- mode: ruby -*-
# vi: set ft=ruby :

# Define the number of worker nodes
num_workers = 2

# Run script to create inventory file
File.open("inventory.ini", "w") do |file|
  file.write("[controller]\n")
  file.write("controller ansible_host=192.168.56.10 ansible_user=vagrant\n")
  file.write("\n")
  file.write("[workers]\n")
  (1..num_workers).each do |i|
    file.write("node#{i} ansible_host=192.168.56.#{i+10} ansible_user=vagrant")
    file.write("\n")
  end
end

# Vagrantfile 
Vagrant.configure("2") do |config|
  # Controller node
  config.vm.define "controller" do |controller|
    controller.vm.box = "bento/ubuntu-20.04"
    controller.vm.box_version = "202404.23.0"
    controller.vm.hostname = "controller"
    controller.vm.network "private_network", ip: "192.168.56.10"

    controller.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end
  end

  # Worker Node(s)
  (1..num_workers).each do |i|
    config.vm.define "node#{i}" do |worker|
      worker.vm.box = "bento/ubuntu-20.04"
      worker.vm.box_version = "202404.23.0"
      worker.vm.hostname = "node#{i}"
      worker.vm.network "private_network", ip: "192.168.56.#{i+10}"

      worker.vm.provider "virtualbox" do |vb|
        vb.memory = 6144
        vb.cpus = 2
      end
    end
  end

  # Provisioning with Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "playbooks/setup_k3d_cluster.yml"
    ansible.inventory_path = "inventory.ini"
  end
end