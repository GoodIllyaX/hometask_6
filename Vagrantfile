# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/ubuntu2204"

  config.vm.disk :disk, size: "500MB", name: "extra_storage1"
  config.vm.disk :disk, size: "600MB", name: "extra_storage2"
  config.vm.disk :disk, size: "400MB", name: "extra_storage3"
  config.vm.disk :disk, size: "400MB", name: "extra_storage4"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y apache2
     
     parted -a optimal --script /dev/sdb  mklabel gpt  mkpart primary ext4 0% 100%  set 1 lvm on
     parted -a optimal --script /dev/sdc  mklabel gpt  mkpart primary ext4 0% 100%  set 1 lvm on

     parted -a optimal --script /dev/sdd mklabel gpt mkpart primary ext4 0% 100% set 1 lvm on
     parted -a optimal --script /dev/sde mklabel gpt mkpart primary ext4 0% 100% set 1 lvm on

     pvcreate /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 
     vgcreate vg_data /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1

     lvcreate -L 800M -n vol0 vg_data
     lvcreate -L 800M -n vol1 vg_data
    
     mkfs.ext4 /dev/vg_data/vol0
     mkfs.ext4 /dev/vg_data/vol1
    
     mkdir -p /mnt/vol0 /mnt/vol1
     echo '/dev/vg_data/vol0 /mnt/vol0 ext4 defaults 0 0' >> /etc/fstab
     echo '/dev/vg_data/vol1 /mnt/vol1 ext4 defaults 0 0' >> /etc/fstab
     mount -a

  SHELL
end
