# -*- mode: ruby -*-
# vi: set ft=ruby :

hostname = 'dev.vippetcare.com'
network_address = '192.168.22.22'

Vagrant.configure(2) do |config|
  config.vm.hostname = hostname

  config.vm.box = 'ubuntu/trusty64'
  config.vm.network :private_network, ip: network_address

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'ansible/playbook.yml'
    ansible.inventory_path = 'ansible/inventory'
    ansible.host_key_checking = 'false'
    ansible.limit = 'all'
  end

  config.vm.provider 'virtualbox' do |vb|
    vb.name = hostname
    vb.memory = 2048
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.synced_folder '.', '/vagrant'
end
