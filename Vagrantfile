# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.

  config.vm.box      = 'trusty'
  config.vm.box_url  = '~/work/boxes/trusty.box'
  config.vm.hostname = 'devbox'
  config.vm.network "private_network",ip: "192.168.59.4"
#  config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"  
  
  config.vm.provision "ansible" do |ansible|
    ansible.groups ={
    "devboxes" => ["default"]
    } 
    ansible.playbook = "provisioning/devbox.yml"
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.verbose = 'vvvv'
    ansible.inventory_path = "provisioning/ansible_hosts"
    ansible.host_key_checking = false
    ansible.extra_vars = { ansible_ssh_user: 'vagrant', 
      ansible_connection: 'ssh',
      ansible_ssh_args: '-o ForwardAgent=yes'}
    
  end
  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true
end
