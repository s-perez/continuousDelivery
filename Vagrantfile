# -*- mode: ruby -*-
Vagrant.configure("2") do |config|
  config.vm.box = "cloud-trusty64"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # See devel.hosts
  machines = [
    { :ip => "192.168.168.10", :name => "ci", :memory => 1024 },
  ]

  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "devel.hosts"
    ansible.playbook = "devel.yml"
    ansible.sudo = true
  end

  machines.each do |machine|
    config.vm.define machine[:name] do |node|
      node.vm.hostname = machine[:name]
      node.vm.network "private_network", ip: machine[:ip]

      if machine.has_key?(:memory)
        node.vm.provider :virtualbox do |v|
          v.memory = machine[:memory]
        end
      end

    end
  end

end
# vi: set ft=ruby :

