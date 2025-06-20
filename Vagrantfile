Vagrant.configure("2") do |config|
  config.vm.provision "shell", path: "script.sh"
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.install_mode = "pip"
  end
    
  config.vm.define "controle" do |controle|
    controle.vm.box = "shekeriev/debian-11"
    controle.vm.hostname = "controle"
    controle.vm.network "private_network", ip: "172.17.177.100"
    controle.vm.provider "virtualbox" do |vb|
      vb.name = "controle"
      vb.memory = "4096"
      vb.cpus = 2
    end
    controle.vm.provision "ansible_local" do |controle|
      controle.playbook = "installjenkins.yml"
      controle.install_mode = "pip"
    end
  end

  config.vm.define "web" do |web|
    web.vm.box = "shekeriev/debian-11"
    web.vm.hostname = "web"
    web.vm.network "private_network", ip: "172.17.177.101"
    web.vm.provider "virtualbox" do |vb|
      vb.name = "web"
      vb.memory = "512"
      vb.cpus = 2
    end
  end

  config.vm.define "db" do |db|
    db.vm.box = "shekeriev/debian-11"
    db.vm.hostname = "db"
    db.vm.network "private_network", ip: "172.17.177.102"
    db.vm.provider "virtualbox" do |vb|
      vb.name = "db"
      vb.memory = "512"
      vb.cpus = 2
    end
  end

  config.vm.define "puppet" do |puppet|
    puppet.vm.box = "shekeriev/debian-11"
    puppet.vm.hostname = "puppet"
    puppet.vm.network "private_network", ip: "172.17.177.200"
    puppet.vm.provider "virtualbox" do |vb|
      vb.name = "puppet"
      vb.memory = "4096"
      vb.cpus = 2
    end
    puppet.vm.provision "shell", inline: "echo 'nameserver 8.8.8.8' > /etc/resolv.conf"
    puppet.vm.provision "puppet" do |puppet|
	puppet.manifests_path = "manifests"
	puppet.manifest_file = "site.pp"
    end
  end
end
