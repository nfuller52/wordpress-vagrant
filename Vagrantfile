# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

variables_path = [File.dirname(__FILE__), '/system/ansible/group_vars/all.yml'].join
variables = YAML::load(File.open(variables_path))

Vagrant.configure(2) do |config|
  config.vm.hostname = variables['site_hostname']

  config.vm.box = 'ubuntu/trusty64'
  config.vm.network :private_network, ip: variables['network_address']

  config.vm.define (variables['name']) { |devel| }

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'system/ansible/playbook.yml'
    ansible.inventory_path = 'system/ansible/inventory'
    ansible.host_key_checking = 'false'
    ansible.limit = 'all'
  end

  config.vm.provider 'virtualbox' do |vb|
    vb.name = variables['site_hostname']
    vb.memory = 2048
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.synced_folder './app', '/vagrant', type: "nfs"
end
