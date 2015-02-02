# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "chef/centos-6.6"

  config.vm.hostname = "dockerhost"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.100.101"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Config the synced folder using NFS if possible.
  # config.vm.synced_folder '.', '/vagrant', :nfs => (RUBY_PLATFORM =~ /linux/ or RUBY_PLATFORM =~ /darwin/)

  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  # VirtualBox
  config.vm.provider "virtualbox" do |v, override|
    v.name = "dockerhost"
    v.memory = 1024
    v.cpus = 2

    # Fix issue with DNS
    # @todo Is this still needed?
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # VMWare Fusion and Workstation
  config.vm.provider "vmware_desktop" do |v, override|
    v.name = "dockerhost"
    v.memory = 1024
    v.cpus = 2
  end

  # Parallels
  config.vm.provider "parallels" do |v, override|
    v.name = "dockerhost"
    v.memory = 1024
    v.cpus = 2
    override.vm.box = "parallels/centos-6.6"
  end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision "chef_solo" do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { mysql_password: "foo" }
  # end

  config.vm.provision "chef_zero" do |chef|
    # Specify the local paths where Chef data is stored
    chef.cookbooks_path = "berks-cookbooks"
    chef.roles_path = "roles"
    chef.nodes_path = "nodes"
    chef.data_bags_path = "data_bags"
    # chef.environments_path = "environments"
    # chef.environment = "dev"
    chef.node_name = "dockerhost"
    chef.add_recipe "docker"
    chef.add_recipe "chef-dk"
    chef.add_recipe "git"

  end

end
