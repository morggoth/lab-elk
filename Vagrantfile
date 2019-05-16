# -*- mode: ruby -*-
# vi: set ft=ruby :

ANSIBLE_RAW_SSH_ARGS = ['-o IdentityFile=./.vagrant/machines/elk/virtualbox/private_key' ]

Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/bionic64'
  config.vm.network 'forwarded_port', guest: 80, host: 8080
  config.vm.hostname = 'elk'
  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '4096'
    vb.cpus = '2'
  end
  config.vm.provision 'shell', inline: <<-SHELL
    apt install python -y
  SHELL
  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'ansible/site.yaml'
    ansible.inventory_path = 'ansible/inventory'
    ansible.become = true
    ansible.limit = 'all'
    ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
  end
end
