The goal: automate making VM (vagrant) and provisioning (ansible)
 On Windows...

tools:
- Windows 10, 11
- virtual box 7.0
- vagrant 2.4.3

VMs:
- Ansible controller
- Server (example a DNS)
- Client(s) (DNS client)


Commands:
```
ssh-keygen -f ans_key
vagrant up
vagrant ssh ubuntu
cd /vagrant
ansible-playbook -i inventory/all.yaml playbook.yml
```
create your ownkey please security


notes:
Sometimes it hangs on "ubuntu: SSH auth method: private key"

next step: 
test vagrant up parallel