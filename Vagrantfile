# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant configuration
Vagrant.configure(2) do |config|
  # CentOS 6.x base box
  config.vm.box = "cedadev/centos6"

  config.vm.host_name = 'ceda-minio'
  config.vm.network "private_network", ip: "192.168.51.30"

  config.vm.synced_folder "/Users/dhk63261/Archive/", "/Archive/"

  config.vm.provision :shell, inline: <<SHELL
set -x

mkdir -p /root/.ssh
cp ~vagrant/.ssh/authorized_keys /root/.ssh

SHELL

  config.vm.provision :ansible do |ansible|
    ansible.force_remote_user = false
    ansible.playbook = "playbook/playbook.yml"
    ansible.inventory_path = "playbook/inventory.ini"
  end
end
