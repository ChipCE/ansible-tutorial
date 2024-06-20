# ansible-tutorial


<pre>
ssh-keygen -t ed25519 -C "magineko default"
ssh-copy-id -i id_ed25519.pub 192.168.1.101
ssh-keygen -t ed25519 -C "ansible tutorial"
ssh-copy-id -i /home/chip/.ssh/ansible.pub 192.168.1.101
ssh -i ~/.ssh/ansible 192.168.1.101

# auto login
eval $(ssh-agent)
ssh-add
# add to .bashrc
alias ssha='eval $(ssh-agent) && ssh-add'
</pre>

inventory : server list

check config
<code>ansible all --key-file ~/.ssh/ansible -i inventory -m ping</code>
with config file
<code>ansible all -m ping</code>
<code>ansible all -m gather_facts</code>
<code>ansible all -m gather_facts --limit 192.168.1.101</code>

* sub node need to have sftp enabled
<pre>
# cat /etc/ssh/sshd_config | grep Subsystem
Subsystem       sftp    /usr/libexec/openssh/sftp-server
</pre>

# elevated ad-hoc Commands
ansible all -m apt -a update_cache=true
ansible all -m apt -a update_cache=true --become --ask-become-pass
# install pkg
ansible all -m apt -a name=neofetch --become --ask-become-pass
# update to latest
ansible all -m apt -a "name=nano state=latest" --become --ask-become-pass
ansible all -m apt -a "upgrade=dist" --become --ask-become-pass

ansible-playbook --ask-become-pass playbook.yml

ansible-playbook --ask-become-pass --tags debian playbook-node.yml