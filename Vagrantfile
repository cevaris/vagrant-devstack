# -*- mode: ruby -*-
# vi: set ft=ruby :

name = 'devstack'
ip_address = '192.168.6.100'

$provision_script = %{
#!/bin/bash

sudo apt-get update
sudo apt-get install unzip vim build-essential git-core curl -y
git clone https://github.com/openstack-dev/devstack.git

}

Vagrant.configure("2") do |config|

  config.vm.define "#{name}" do |node|
    
    node.vm.box = "precise64"
    node.vm.box_url = "http://goo.gl/sHRjNb"

    
    node.vm.provider :virtualbox do |v|
      v.name = "#{name}"
      v.customize ["modifyvm", :id, '--memory', '4096']
    end

    node.vm.network :private_network, ip: ip_address
    node.vm.hostname = "#{name}"
    node.vm.provision :shell, :inline => $provision_script
  end

end