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

  # configure two machines server1 & server2
  (1..2).each do |i|
    config.vm.define "server#{i}.lab.local" do |node|

      # machine basic settings
      node.vm.box = "centos/8"
      node.vm.box_version = "2011.00"
      node.vm.hostname = "server#{i}.lab.local"
      # yes this is a bug in Vagrant: we need to provide the ip-address even if auto_config doesn't use it
      node.vm.network "private_network", ip: "192.168.56.2#{i}0", auto_config: false
      # provider specific settings
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"

        # Get disk path
        vb.name = "server#{i}.lab.local"
        line = `VBoxManage list systemproperties | grep "Default machine folder"`
        vb_machine_folder = line.split(':')[1].strip()

        disk2_name = "disk2.vd1"
        disk3_name = "disk3.vd1"

        second_disk = File.join(vb_machine_folder, vb.name, disk2_name)
        third_disk = File.join(vb_machine_folder, vb.name, disk3_name)

        vb.customize ["storagectl", :id, "--name", "SATA Controller", "--add", "sata"]

        # Add two more disks
        unless File.exist?(second_disk)
          vb.customize ['createhd', '--filename', second_disk, '--variant', 'Fixed', '--size', 16 * 1024]
        end
        unless File.exist?(third_disk)
          vb.customize ['createhd', '--filename', third_disk, '--variant', 'Fixed', '--size', 16 * 1024]
        end

        # attach the new disks
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', second_disk]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', third_disk]
      end

    end
  end

end
