# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define 'database' do |db|
    db.vm.box = "generic/ubuntu2004"
    db.ssh.insert_key = false
    db.ssh.username = "vagrant"
    db.vm.network "private_network", ip: "192.168.50.10"
    db.vm.hostname = "database"
    db.vm.synced_folder ".", "/vagrant"
    db.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = 1024
      vb.linked_clone = false
    end

    db.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "database.yaml"
      ansible.galaxy_role_file = 'requirements.yaml'
      ansible.galaxy_roles_path = '/vagrant/.ansible/roles'
      ansible.galaxy_command = 'ansible-galaxy collection install community.mysql'
    ansible.verbose="v"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3.8" }
    end
  end
  config.vm.define 'wordpress1' do |wp|
    wp.vm.box = "generic/ubuntu2004"
    wp.ssh.insert_key = false
    wp.ssh.username = "vagrant"
    wp.vm.network "private_network", ip: "192.168.50.21"
    wp.vm.hostname = "wordpress"
    wp.vm.synced_folder ".", "/vagrant"
    wp.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = 512
      vb.linked_clone = false
    end

    wp.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "wordpress.yaml"
    ansible.verbose="v"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3.8" }
    end
  end
  config.vm.define 'wordpress2' do |wp|
    wp.vm.box = "generic/ubuntu2004"
    wp.ssh.insert_key = false
    wp.ssh.username = "vagrant"
    wp.vm.network "private_network", ip: "192.168.50.22"
    wp.vm.hostname = "wordpress"
    wp.vm.synced_folder ".", "/vagrant"
    wp.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = 512
      vb.linked_clone = false
    end

    wp.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "wordpress.yaml"
    ansible.verbose="v"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3.8" }
    end
  end
  config.vm.define 'lb' do |lb|
    lb.vm.box = "generic/ubuntu2004"
    lb.ssh.insert_key = false
    lb.ssh.username = "vagrant"
    lb.vm.network "private_network", ip: "192.168.50.2"
    lb.vm.hostname = "wordpress"
    lb.vm.synced_folder ".", "/vagrant"
    lb.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = 512
      vb.linked_clone = false
    end

    lb.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "lb.yaml"
    ansible.verbose="v"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3.8" }
    end
  end
end
