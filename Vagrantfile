Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"
  config.vm.box = "bento/centos-6.6"
  config.vm.define "node1" do |machine|
    machine.vm.network "private_network", ip: "172.17.177.21"
	machine.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "4096"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
	end
  end
  config.vm.define "node2" do |machine|
    machine.vm.network "private_network", ip: "172.17.177.22"
	machine.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "4096"]
          vb.customize ["modifyvm", :id, "--cpus", "2"]
    end
  end
  config.vm.define 'controller' do |machine|
    machine.vm.network "private_network", ip: "172.17.177.11"

    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "main.yml"
      ansible.verbose        = true
      ansible.install        = true
      ansible.limit          = "nodes"
      ansible.inventory_path = "inventory"
	  ansible.raw_arguments  = ["--connection=paramiko"]
    end
  end
  
end
