# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :virtualbox do |v|
    v.name = "jenkins"
    v.memory = 512
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "jenkins"
  config.vm.network :private_network, ip: "192.168.33.55"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :jenkins do |jenkins|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/jenkins-box.yml"
    ansible.inventory_path = "playbooks/inventory/jenkins-inventory.yml"
    ansible.vault_password_file = "vault-qa-password"
    ansible.become = true
  end

end
