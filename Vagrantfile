# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "centos6.5"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "sufia.local"

  # If true, then any SSH connections made will enable agent forwarding.
  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
  end

  # unfortunate workaround 
  # Ansible doesn't work with Vagrant from a Windows host
  config.vm.provision "shell", inline: "yum -y install ansible python-setuptools"
  config.vm.synced_folder "./", "/etc/ansible",
    owner: "root",
    group: "root",
    mount_options: ["dmode=775,fmode=664"]
  config.vm.provision "shell", inline: "export PYTHONUNBUFFERED=1 && ansible-playbook -i /etc/ansible/vagrant /etc/ansible/sufia.yml --connection=local"


end
