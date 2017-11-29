# -*- mode: ruby -*-
# vi: set ft=ruby :

#require necessary plugins
required_plugins = %w( vagrant-hostmanager vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true

  config.vm.define "boxa1" do |b|
    b.vm.box = "ubuntu/xenial64" # 16.04
    b.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    b.vm.synced_folder ".", "/vagrant", disabled: true
    b.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    #b.vm.synced_folder "docker-images", "/home/ubuntu/docker-images", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    b.vbguest.auto_update = true

    b.vm.network "private_network", ip: "192.168.50.11", virtualbox__intnet: "networka"
    b.vm.network "private_network", ip: "192.168.70.11", virtualbox__intnet: "networkc"
    b.vm.network "public_network", type: "dhcp", bridge: "en0: WLAN (AirPort)"

    b.vm.hostname = "boxa1.locala.dev"
    #b.hostmanager.aliases = %w(node-1.local.dev)

    b.vm.provision "ansible_local" do |ansible|
      ansible.install = true
      ansible.install_mode = :pip
      ansible.version = "latest"
      ansible.playbook = "ansible/playbook-a1.yml"
      ansible.galaxy_role_file = "ansible/requirements.yml"
    end
  end
  config.vm.define "boxa2" do |b|
    b.vm.box = "ubuntu/xenial64" # 16.04
    b.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    b.vm.synced_folder ".", "/vagrant", disabled: true
    b.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    #b.vm.synced_folder "docker-images", "/home/ubuntu/docker-images", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    b.vbguest.auto_update = true

    b.vm.network "private_network", ip: "192.168.50.12", virtualbox__intnet: "networka"
    #b.vm.network "private_network", type: "dhcp"
    b.vm.hostname = "boxa2.locala.dev"
    #b.hostmanager.aliases = %w(node-1.local.dev)

    b.vm.provision "ansible_local" do |ansible|
      ansible.install = true
      ansible.install_mode = :pip
      ansible.version = "latest"
      ansible.playbook = "ansible/playbook-a2.yml"
      ansible.galaxy_role_file = "ansible/requirements.yml"
    end
  end

  config.vm.define "boxb1" do |b|
    b.vm.box = "ubuntu/xenial64" # 16.04
    b.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    b.vm.synced_folder ".", "/vagrant", disabled: true
    b.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    #b.vm.synced_folder "docker-images", "/home/ubuntu/docker-images", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    b.vbguest.auto_update = true

    b.vm.network "private_network", ip: "192.168.60.11", virtualbox__intnet: "networkb"
    b.vm.network "private_network", ip: "192.168.70.12", virtualbox__intnet: "networkc"
    #b.vm.network "private_network", type: "dhcp"
    b.vm.hostname = "boxb1.localb.dev"
    #b.hostmanager.aliases = %w(node-1.local.dev)

    b.vm.provision "ansible_local" do |ansible|
      ansible.install = true
      ansible.install_mode = :pip
      ansible.version = "latest"
      ansible.playbook = "ansible/playbook-b1.yml"
      ansible.galaxy_role_file = "ansible/requirements.yml"
    end
  end
  config.vm.define "boxb2" do |b|
    b.vm.box = "ubuntu/xenial64" # 16.04
    b.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    b.vm.synced_folder ".", "/vagrant", disabled: true
    b.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    #b.vm.synced_folder "docker-images", "/home/ubuntu/docker-images", create: true, owner: "ubuntu", group: "ubuntu", mount_options: ["dmode=777,fmode=777"]
    b.vbguest.auto_update = true

    b.vm.network "private_network", ip: "192.168.60.12", virtualbox__intnet: "networkb"
    #b.vm.network "private_network", type: "dhcp"
    b.vm.hostname = "boxb2.localb.dev"
    #b.hostmanager.aliases = %w(node-1.local.dev)

    b.vm.provision "ansible_local" do |ansible|
      ansible.install = true
      ansible.install_mode = :pip
      ansible.version = "latest"
      ansible.playbook = "ansible/playbook-b2.yml"
      ansible.galaxy_role_file = "ansible/requirements.yml"
    end
  end
end
