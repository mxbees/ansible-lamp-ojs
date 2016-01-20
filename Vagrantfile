# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "debian8"
  config.vm.box_url = "https://github.com/holms/vagrant-jessie-box/releases/download/Jessie-v0.1/Debian-jessie-amd64-netboot.box"
  
  config.vm.host_name = "ojs3"

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.network :private_network, ip: "10.10.10.10"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
