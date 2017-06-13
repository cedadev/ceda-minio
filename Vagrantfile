# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant configuration
Vagrant.configure(2) do |config|
  # CentOS 6.x base box
  config.vm.box = "cedadev/centos68"

  config.vm.host_name = 'ceda-minio'
  config.vm.network "private_network", ip: "192.168.51.30"

  config.vm.synced_folder "/Users/dhk63261/Archive/", "/Archive/"

  config.vm.provision :shell, inline: <<SHELL
set -x

mkdir -p /root/.ssh
cp ~vagrant/.ssh/authorized_keys /root/.ssh

cat > /etc/selinux/config <<-SELINUXCONF
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings instead of enforcing.
#       disabled - SELinux is fully disabled.
SELINUX=disabled
# SELINUXTYPE= type of policy in use. Possible values are:
#       targeted - Only targeted network daemons are protected.
#       strict - Full SELinux protection.
SELINUXTYPE=targeted
SELINUXCONF
SHELL

  # Disabling SELinux requires a reboot
  #   Requires "vagrant plugin install vagrant-reload"
  config.vm.provision :reload

  config.vm.provision :ansible do |ansible|
    ansible.force_remote_user = false
    ansible.playbook = "playbook/playbook.yml"
    ansible.inventory_path = "playbook/inventory.ini"
  end
end
