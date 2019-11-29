$hosts_script = <<SCRIPT
apt-get update
apt-get -q -y install python
git clone https://github.com/ameizi/docker-rabbitmq-cluster.git
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "rabbitmq"
  config.vm.define "rabbitmq"
  config.vm.provider :virtualbox do |v|
    v.name = "rabbitmq"
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end
  config.vm.network :private_network, ip: "10.211.55.126"
  config.vm.provision :shell, :inline => $hosts_script

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible/site.yml"
    ansible.inventory_path = "ansible/hosts"
  end

end
