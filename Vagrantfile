# -*- mode: ruby -*-
# vi: set ft=ruby :

$pre_provision = <<SCRIPT
export DEBIAN_FRONTEND=noninteractive
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install python gnupg
SCRIPT

Vagrant.configure("2") do |config|
    config.vm.box = "debian/buster64"

    config.vm.network "forwarded_port", guest: 8888, host: 8888

    config.vm.provision "shell", inline: $pre_provision
    config.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.galaxy_role_file = "provisioning/roles.yml"
        ansible.playbook = "provisioning/playbook.yml"
    end
end
