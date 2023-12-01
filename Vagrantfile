# -*- mode: ruby -*-
# vi: set ft=ruby :

$scriptbullseye = <<-SCRIPTBULLSEYE
apt update
apt install -y gpg
apt install locales
locale-gen en_US.UTF-8
apt install -y emacs-nox
apt install -y python3-pip
apt install -y python3-venv
sudo -i -u vagrant bash -c "python3 -m venv ~/venv-ansible"
sudo -i -u vagrant bash -c "pip3 install -U pip"
sudo -i -u vagrant bash -c "pip3 install -U ansible"
SCRIPTBULLSEYE

$scriptjammy = <<-SCRIPTJAMMY
apt update
apt install -y gpg
#apt install -y emacs-nox
#apt install -y python3-pip
#apt install -y python3.10-venv
#sudo -i -u vagrant bash -c "python3 -m venv ~/venv-ansible"
#sudo -i -u vagrant bash -c "pip3 install -U pip"
#sudo -i -u vagrant bash -c "pip3 install -U ansible"
SCRIPTJAMMY

$scriptrockylinux = <<-SCRIPTROCKYLINUX
dnf update
dnf install -y emacs-nox python3-pip
sudo -i -u vagrant bash -c "python -m venv ~/venv-ansible"
sudo -i -u vagrant bash -c "pip install -U pip"
sudo -i -u vagrant bash -c "pip install -U ansible"
SCRIPTROCKYLINUX

Vagrant.configure('2') do |config|

  ENV['LC_ALL']="en_US.UTF-8"
  ENV['LC_LCTYPE']="en_US.UTF-8"

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://pfrie-std.proxy.e2.rie.gouv.fr:8080"
    config.proxy.https    = "http://pfrie-std.proxy.e2.rie.gouv.fr:8080"
    config.proxy.no_proxy = "localhost,127.0.0.1,.e2.rie.gouv.fr"
  end

  # Ensure we use our vagrant private key
  config.ssh.insert_key = false
  config.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'

  #             _          ____ 
  #  __ ___ _ _| |_ ___ __|__  |
  # / _/ -_) ' \  _/ _ (_-< / / 
  # \__\___|_||_\__\___/__//_/  
  #                             

#  config.vm.define 'centos7.local' do |machine|

#    machine.vm.box = "centos/7"
#    machine.vm.network :private_network, ip: '192.168.88.24'
#    machine.vm.hostname = 'centos7.local'

#    machine.vm.provision 'file' do |file|
#      file.source = "~/.vagrant.d/insecure_private_key"
#      file.destination = "~/.vagrant.d/insecure_private_key"
#    end
    
#    machine.vm.provision 'shell' do |shell|
#      shell.inline = "echo toto"
#      #shell.inline = $scriptbullseye
#    end

#    machine.vm.provision 'ansible' do |ansible|
#      ansible.playbook = 'tests/playbook.yml'
#      #ansible.verbose = "vvv"
#      ansible.become = true
#      ansible.inventory_path = 'vagrant-inventory'
#      ansible.host_key_checking = false
#    end

#  end

  #  _         _ _                  
  # | |__ _  _| | |___ ___ _  _ ___ 
  # | '_ \ || | | (_-</ -_) || / -_)
  # |_.__/\_,_|_|_/__/\___|\_, \___|
  #                        |__/     
  
#  config.vm.define 'bullseye64.local' do |machine|

#    machine.vm.box = "debian/bullseye64"
#    machine.vm.network :private_network, ip: '192.168.88.23'
#    machine.vm.hostname = 'bullseye64.local'

#    machine.vm.provision 'file' do |file|
#      file.source = "~/.vagrant.d/insecure_private_key"
#      file.destination = "~/.vagrant.d/insecure_private_key"
#    end
    
#    machine.vm.provision 'shell' do |shell|
#      shell.inline = "echo toto"
#      #shell.inline = $scriptbullseye
#    end

#    machine.vm.provision 'ansible' do |ansible|
#      ansible.playbook = 'tests/playbook.yml'
#      #ansible.verbose = "vvv"
#      ansible.become = true
#      ansible.inventory_path = 'vagrant-inventory'
#      ansible.host_key_checking = false
#    end

# end

  #    _                      
  #   (_)__ _ _ __  _ __ _  _ 
  #   | / _` | '  \| '  \ || |
  #  _/ \__,_|_|_|_|_|_|_\_, |
  # |__/                 |__/ 

  # config.vm.define 'jammy64.local' do |machine|

  #   machine.vm.box = "ubuntu/jammy64"
  #   machine.vm.network :private_network, ip: '192.168.88.22'
  #   machine.vm.hostname = 'jammy64.local'

  #   machine.vm.provision 'file' do |file|
  #     file.source = "~/.vagrant.d/insecure_private_key"
  #     file.destination = "~/.vagrant.d/insecure_private_key"
  #   end
    
  #   machine.vm.provision 'shell' do |shell|
  #     shell.inline = "echo toto"
  #     #shell.inline = $scriptjammy
  #   end

  #   machine.vm.provision 'ansible' do |ansible|
  #     ansible.playbook = 'tests/playbook.yml'
  #     #ansible.verbose = "vvv"
  #     ansible.become = true
  #     ansible.inventory_path = 'vagrant-inventory'
  #     ansible.host_key_checking = false
  #   end

  # end

#              _        _ _              
#  _ _ ___  __| |___  _| (_)_ _ _  ___ __
# | '_/ _ \/ _| / / || | | | ' \ || \ \ /
# |_| \___/\__|_\_\\_, |_|_|_||_\_,_/_\_\
#                  |__/                  

 config.vm.define 'rockylinux9.local' do |machine|

   machine.vm.box = "rockylinux/9"
   machine.vm.network :private_network, ip: '192.168.88.25'
   machine.vm.hostname = 'rockylinux9.local'

   machine.vm.provision 'file' do |file|
     file.source = "~/.vagrant.d/insecure_private_key"
     file.destination = "~/.vagrant.d/insecure_private_key"
   end
    
   machine.vm.provision 'shell' do |shell|
     #shell.inline = "echo toto"
     shell.inline = $scriptrockylinux
   end

    machine.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'tests/playbook.yml'
      ansible.verbose = "vvv"
      ansible.become = true
      ansible.inventory_path = 'vagrant-inventory'
      ansible.host_key_checking = false
    end

 end

end
