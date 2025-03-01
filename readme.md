The goal: automate making VM (vagrant) and provisioning (ansible)
 On Windows...

tools:
- Windows 10, 11
- virtual box
- vagrant

VMs:
- Ansible controller
- Server (example a DNS)
- Client(s) (DNS client)


Commands:
```
ssh-keygen -f ans_key
vagrant up
vagrant ssh ubuntu

ansible-playbook -i inventory/ playbook.yml
```
create your ownkey please security


notes:
Sometimes it hangs on "ubuntu: SSH auth method: private key"

next step: i need to create an ssh config for the ansible controller