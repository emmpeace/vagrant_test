$script = <<-SCRIPT
sudo apt update
sudo apt install software-properties-common -y
sudo add-apt-repository --yes --update ppa:ansible/ansible
echo installing ansible
sudo apt install ansible -y

wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
echo installing vagrant
sudo apt install vagrant -y
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/jammy64"
    ubuntu.vm.hostname = "vub01"
    ubuntu.vm.network "private_network", ip: "192.168.50.101"
#    ubuntu.vm.network "private_network", type: "dhcp"
    config.vm.provider "virtualbox" do |v|
      v.memory = 8192
      v.cpus = 2
    end

    ubuntu.vm.provision "shell", inline: $script

#    ubuntu.vm.provision "shell", inline: "apt update && apt upgrade -y"
  end

  # config.vm.define "centos" do |centos|
  #   centos.vm.box = "centos/stream8"
  #   centos.vm.hostname = "vce01"
  # end

  # config.vm.define "centos7" do |centos7|
  #   centos7.vm.box = "centos/7"
  #   centos7.vm.hostname = "vce7"
  #   centos7.vm.network "private_network", type: "dhcp"
  # end

  # config.vm.define "centos6" do |centos6|
  #   centos6.vm.box = "bento/centos-6.7"
  #   centos6.vm.hostname = "vce6"
  #   centos6.vm.network "private_network", type: "dhcp"
  # end
  # config.vm.provision "ansible" do |ansible|
  #   ansible.playbook = "playbook.yml"
  # end
end
