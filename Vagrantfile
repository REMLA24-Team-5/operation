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
  # --- Control Node ---
  config.vm.define "controller" do |control|
    control.vm.box = "bento/ubuntu-22.04"
    control.vm.box_version = "202404.23.0"
    control.vm.hostname = "controller"
    control.vm.network "private_network", ip: "192.168.56.10"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2 # had issues running with 1
    end
    
    # setup controller with ansible playbook
    control.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.inventory_path = "inventory.ini"
      ansible.playbook = "playbooks/setup_general.yml"
    end

    # setup cluster
    control.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.inventory_path = "inventory.ini"
      ansible.playbook = "playbooks/setup_cluster.yml"
    end

    # install monitoring tools
    control.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.inventory_path = "inventory.ini"
      ansible.playbook = "playbooks/monitoring.yml"
    end
  end
  
  # --- Worker Nodes ---
  (1..n_workers).each do |i|
    config.vm.define "node#{i}" do |worker|
      worker.vm.box = "bento/ubuntu-22.04"
      worker.vm.box_version = "202404.23.0"
      worker.vm.hostname = "node#{i}"
      worker.vm.network "private_network", ip: "192.168.56.#{i+10}"

      worker.vm.provider "virtualbox" do |vb|
        vb.memory = 6144
        vb.cpus = 2
      end
      
      # setup worker node with ansible playbook
      worker.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.inventory_path = "inventory.ini"
        ansible.playbook = "playbooks/setup_general.yml"
      end

      # join worker node in cluster
      worker.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.inventory_path = "inventory.ini"
        ansible.playbook = "playbooks/node.yml"
      end
    end
  end
end
