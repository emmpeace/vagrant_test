$script = <<-SCRIPT
ans_k=`cat /vagrant/ans_key.pub`
echo "${ans_k}" >> /home/vagrant/.ssh/authorized_keys
SCRIPT

$script2 = <<-SCRIPT
echo preparations for ansible
cp /vagrant/ans_key /home/vagrant/.ssh/id_ed25519
chmod 400 /home/vagrant/.ssh/id_ed25519
chown vagrant:vagrant /home/vagrant/.ssh/id_ed25519
sudo apt update
sudo apt install software-properties-common -y
sudo add-apt-repository --yes --update ppa:ansible/ansible
echo installing ansible
sudo apt install ansible python3-pip python3-passlib -y
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/jammy64"
    ubuntu.vm.hostname = "vub01"
    ubuntu.vm.network "private_network", ip: "192.168.50.101"
#    ubuntu.vm.network "private_network", type: "dhcp"
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end
    ubuntu.vm.provision "shell", inline: $script
    ubuntu.vm.provision "shell", inline: $script2

#    ubuntu.vm.provision "shell", inline: "apt update && apt upgrade -y"
  end

  config.vm.define "ubuntu2" do |ubuntu2|
    ubuntu2.vm.box = "ubuntu/jammy64"
    ubuntu2.vm.hostname = "vub02"
    ubuntu2.vm.network "private_network", ip: "192.168.50.102"
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end
    ubuntu2.vm.provision "shell", inline: $script
  end

  config.vm.define "ubuntu3" do |ubuntu3|
    ubuntu3.vm.box = "ubuntu/jammy64"
    ubuntu3.vm.hostname = "vub03"
    ubuntu3.vm.network "private_network", ip: "192.168.50.103"
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end
    ubuntu3.vm.provision "shell", inline: $script
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

## commands
#sudo apt -y install bridge-utils cpu-checker libvirt-clients libvirt-daemon qemu qemu-kvm virt-manager
#sudo virt-install --name ubuntu-guest --os-variant ubuntu20.04 --vcpus 2 --ram 2048 --location http://ftp.ubuntu.com/ubuntu/dists/focal/main/installer-amd64/ --network bridge=virbr0,model=virtio --graphics none --extra-args='console=ttyS0,115200n8 serial'
