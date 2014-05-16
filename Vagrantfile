# -*- mode: ruby -*-
# vi: set ft=ruby :

name = 'devstack'
ip_address = '10.0.0.100'

$provision_script = %{
#!/bin/bash

sudo apt-get update
sudo apt-get install unzip vim build-essential git-core curl -y

rm -r devstack
git clone https://github.com/openstack-dev/devstack.git
cd devstack

cat >local.conf <<EOL
[[local|localrc]]
FLOATING_RANGE=192.168.1.224/27
FIXED_RANGE=10.11.12.0/24
FIXED_NETWORK_SIZE=256
FLAT_INTERFACE=eth0
ADMIN_PASSWORD=supersecret
MYSQL_PASSWORD=iheartdatabases
RABBIT_PASSWORD=flopsymopsy
SERVICE_PASSWORD=iheartksl
EOL

# sudo adduser stack
# sudo echo "stack ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
# sudo chown stack ./.* ./*
# sudo su stack
# ./stack.sh
# shucks

}

Vagrant.configure("2") do |config|

  config.vm.define "#{name}" do |node|
    
    node.vm.box = "precise64"
    node.vm.box_url = "http://goo.gl/sHRjNb"

    
    node.vm.provider :virtualbox do |v|
      v.name = "#{name}"
      v.customize ["modifyvm", :id, '--memory', '5120']
    end

    node.vm.network :private_network, ip: ip_address
    node.vm.hostname = "#{name}"
    node.vm.provision :shell, :inline => $provision_script
  end

end