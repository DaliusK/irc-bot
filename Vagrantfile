Vagrant.require_version ">= 1.5"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  vm_name = "irc-bot"

  config.vm.provider "virtualbox" do |v|
    v.name = vm_name
    v.customize [
      "modifyvm", :id,
      "--name", vm_name,
      "--memory", 1024,
      "--natdnshostresolver1", "on",
      "--cpus", 1,
    ]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.inventory_path = "ansible/inventories/dev"
    ansible.limit = 'vm'
  end
end
