Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "pihole"

  # Add private network
  config.vm.network "private_network", ip: "192.168.56.10"

  # Fix locale first
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y language-pack-en
    sudo update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8
    export LANG=en_US.UTF-8
    export LC_ALL=en_US.UTF-8
  SHELL

  # Ansible provisioner
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "master_playbook.yml"
    ansible.inventory_path = "inventory-test"
    ansible.limit = "pihole"

  end
end

