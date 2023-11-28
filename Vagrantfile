# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://pfrie-std.proxy.e2.rie.gouv.fr:8080"
    config.proxy.https    = "http://pfrie-std.proxy.e2.rie.gouv.fr:8080"
    config.proxy.no_proxy = "localhost,127.0.0.1"
  end
  
  # Ensure we use our vagrant private key
  config.ssh.insert_key = false
  config.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'

  config.vm.define 'jammy64.local' do |machine|

    machine.vm.box = "ubuntu/jammy64"
    machine.vm.network :private_network, ip: '192.168.88.22'
    machine.vm.hostname = 'jammy64.local'

    machine.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'tests/playbook.yml'
      ansible.verbose = "vvv"
      ansible.become = true
      ansible.inventory_path = 'vagrant-inventory'
      ansible.host_key_checking = false
    end

  end

end
