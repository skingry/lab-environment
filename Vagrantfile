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

  # configure server1
  config.vm.define "server1.example.com" do |node|

    # machine basic settings
    node.vm.box = "centos/8"
    node.vm.box_version = "2011.00"
    node.vm.hostname = "server1.example.com"
    # yes this is a bug in Vagrant: we need to provide the ip-address even if auto_config doesn't use it
    node.vm.network "private_network", ip: "192.168.0.110", auto_config: false
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
  end

  # configure server1
  config.vm.define "server2.example.com" do |node|

    # machine basic settings
    node.vm.box = "centos/8"
    node.vm.box_version = "2011.00"
    node.vm.hostname = "server2.example.com"
    # yes this is a bug in Vagrant: we need to provide the ip-address even if auto_config doesn't use it
    node.vm.network "private_network", ip: "192.168.0.120", auto_config: false
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"

      # Get disk path
      vb.name = "server2.example.com"
      line = `VBoxManage list systemproperties | grep "Default machine folder"`
      vb_machine_folder = line.split(':')[1].strip()

      disk2_name = "disk2.vd1"
      disk3_name = "disk3.vd1"
      disk4_name = "disk4.vd1"
      disk5_name = "disk5.vd1"
      disk6_name = "disk6.vd1"
      disk7_name = "disk7.vd1"
      disk8_name = "disk8.vd1"

      second_disk  = File.join(vb_machine_folder, vb.name, disk2_name)
      third_disk   = File.join(vb_machine_folder, vb.name, disk3_name)
      fourth_disk  = File.join(vb_machine_folder, vb.name, disk4_name)
      fifth_disk   = File.join(vb_machine_folder, vb.name, disk5_name)
      sixth_disk   = File.join(vb_machine_folder, vb.name, disk6_name)
      seventh_disk = File.join(vb_machine_folder, vb.name, disk7_name)
      eighth_disk  = File.join(vb_machine_folder, vb.name, disk8_name)

      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--portcount', 8]

      # Add two more disks
      unless File.exist?(second_disk)
        vb.customize ['createhd', '--filename', second_disk, '--variant', 'Fixed', '--size', 250]
      end
      unless File.exist?(third_disk)
        vb.customize ['createhd', '--filename', third_disk, '--variant', 'Fixed', '--size', 250]
      end
      unless File.exist?(fourth_disk)
        vb.customize ['createhd', '--filename', fourth_disk, '--variant', 'Fixed', '--size', 250]
      end
      unless File.exist?(fifth_disk)
        vb.customize ['createhd', '--filename', fifth_disk, '--variant', 'Fixed', '--size', 250]
      end
      unless File.exist?(sixth_disk)
        vb.customize ['createhd', '--filename', sixth_disk, '--variant', 'Fixed', '--size', 4096]
      end
      unless File.exist?(seventh_disk)
        vb.customize ['createhd', '--filename', seventh_disk, '--variant', 'Fixed', '--size', 1024]
      end
      unless File.exist?(eighth_disk)
        vb.customize ['createhd', '--filename', eighth_disk, '--variant', 'Fixed', '--size', 1024]
      end

      # attach the new disks
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', second_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', third_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', fourth_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 5, '--device', 0, '--type', 'hdd', '--medium', fifth_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 6, '--device', 0, '--type', 'hdd', '--medium', sixth_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 7, '--device', 0, '--type', 'hdd', '--medium', seventh_disk]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 8, '--device', 0, '--type', 'hdd', '--medium', eighth_disk]

    end
  end
end
