# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.8"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  # Give it a name to make it clear which machine `vagrant status` refers to
  config.vm.define "ckan" do |ckan|
    ckan.vm.network "private_network", ip: "192.168.19.97"
    ckan.vm.hostname = "ckan.lo"
    ckan.vm.synced_folder ".", "/vagrant", type: "nfs"
    ckan.vm.provision "provision_ckan", type: "shell" do |provision|
      provision.path = "vagrant/package_provision.sh"
      # provision.privileged = false
      # provision.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
    end
    ckan.vm.provider "virtualbox" do |v|
      v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant-root", "1"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--cpus", 1]
    end
    ckan.ssh.forward_agent = true
  end
end
