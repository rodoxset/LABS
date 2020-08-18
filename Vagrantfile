# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  ## Escolha da Box
  config.vm.box = "ubuntu/bionic64"

  ## Cliente - VM Alvo para configuracao da Playbook do Ansible
  config.vm.define 'cliente' do |cliente|
    cliente.vm.network "private_network", ip: "172.17.177.21"
    cliente.vm.hostname = "cliente" # Hostname da VM

  # Configurações de Size da VM
  cliente.vm.provider "virtualbox" do |v|
     v.name = "Cliente" # Nome no Virtualbox
     v.memory = 1024
     v.cpus = 2
    end
  end

  ## Containers
  config.vm.define 'containers' do |containers|
  containers.vm.network "private_network", ip: "172.17.177.22"
      containers.vm.hostname = "containers" # Hostname da VM

     # Configurações de Size da VM
     containers.vm.provider "virtualbox" do |v|
        v.name = "Containers" # Nome no Virtualbox
        v.memory = 1024
       v.cpus = 2
      end
  
  # Configura a VM
  containers.vm.provision :ansible_local do |ansible|
       ansible.install_mode = "default"
       ansible.playbook = "ansible/playbook.yml"
       ansible.verbose  = true
       ansible.install  = true
       ansible.limit    = "all" 
       ansible.inventory_path = "ansible/inventory"
      end
  end
end