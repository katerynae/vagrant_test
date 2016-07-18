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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos/7"

  config.ssh.forward_agent = true
  # config.ssh.forward_x11 = true
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
  
 config.vm.network "private_network", ip: "10.10.1.130"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder "/opt/pythonenv", "/opt/pythonenv",
    owner: "ordergroove", group: "dev"
  config.vm.synced_folder "~/db_dumps", "/home/ordergroove/db_dumps"
  config.vm.synced_folder "~/whiskey_settings", "/home/ordergroove/whiskey_settings"
  config.vm.synced_folder "~/fernet_settings", "/home/ordergroove/fernet_settings"

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

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update -y

    sudo yum install -y httpd
    sudo yum install -y python-devel

    sudo yum install -y mariadb-server
    sudo systemctl enable mariadb
    sudo systemctl start mariadb
    #sudo touch /etc/yum.repos.d/mongodb-org-3.2.repo
    #sudo yum install -y mongodb-org
    sudo yum install gcc
    sudo yum install httpd httpd-devel mod_ssl mod_wsgi
    sudo service mongod start
    sudo yum install openssl-devel
    sudo yum install xmlsec1
    sudo yum install xmlsec1-openssl
    sudo yum install wget
    sudo yum update && yum install yum-utils    

    yum-config-manager --add-repo http://dl.fedoraproject.org/pub/epel/6/x86_64/
    rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-6
    yum install libxml2 libxml2-devel #(2.7.6)
    yum install libxslt-devel #(1.1.26-2.el6_3.1)
    yum install xmlsec1 xmlsec1-devel #(1.2.16-2.el6)
    yum install xmlsec1-openssl xmlsec1-openssl-devel #(1.2.16-2.el6)
    yum install openssl openssl-devel #(1.0.0-27.el6_4.2)
    yum install libmcrypt-devel #(2.5.8-9.el6)
    yum install libtool-ltdl-devel #(2.2.6-15.5.el6)
    yum install redis #(2.4.10-1.el6)

    sudo yum install rabbitmq-server 
    sudo yum install redis
    sudo yum install memcached
    sudo mkdir -p /var/log/ordergroove
    sudo chown ordergroove:dev /var/log/ordergroove
     ### import the db
    # mysql -e "CREATE DATABASE ogv2_staging"
    # mysql ogv2_staging < /home/vagrant/db_dumps/dump.ogv2_staging.sql

    # install tools
    sudo yum install -y vim
  SHELL
end
