Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define 'dev' do |machine|
    machine.vm.synced_folder "./apps", "/home/vagrant/apps"
    machine.vm.synced_folder "./ansible", "/home/vagrant/ansible"
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    machine.vm.provider "virtualbox" do |v|
      v.memory = 4048
      v.cpus = 2
      v.name = "dev"
      v.customize ["--natdnshostresolver1", "on"]
    end
    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook          = "playbook.yml"
      ansible.provisioning_path = "/home/vagrant/ansible"
      ansible.verbose           = true
      ansible.install           = true
      ansible.limit             = "all" # or only "nodes" group, etc.
      ansible.inventory_path    = "inventory"
    end
  end

end


