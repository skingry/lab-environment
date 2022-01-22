# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # if vagrant-vbguest is installed stop auto updating virtualbox guest add-on update
  if defined? VagrantVbguest
    config.vbguest.auto_update = false
  end

  # Set language locale environment variables
  ENV['LC_ALL']="en_US.UTF-8"
  ENV['LANG']="en_US.UTF-8"

  # login as user1
  config.ssh.username = "user1"

  # disable synced folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # configure server1
  config.vm.define "server1" do |node|
    # machine basic settings
    node.vm.box = "skingry/rhcsa_lab-server1"
    node.vm.box_version = "1"
    node.vm.hostname = "server1.example.com"
    node.vm.network "private_network", ip: "192.168.0.110", auto_config: true
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "rhcsa_lab-server1"
    end
  end

  # configure server2
  config.vm.define "server2" do |node|
    # machine basic settings
    node.vm.box = "skingry/rhcsa_lab-server2"
    node.vm.box_version = "1"
    node.vm.hostname = "server2.example.com"
    node.vm.network "private_network", ip: "192.168.0.120", auto_config: true
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.name = "rhcsa_lab-server2"
    end
  end
end
