In Ansible, the hosts file (also called the inventory file) is where you define the list of managed nodes (servers, VMs, containers — anything Ansible should control).

<pre><code>vim /etc/ansible/hosts</code></pre>

Example of host file 
<pre><code>
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com ansible_user=ansible ansible_port=2222

[all:vars]
ansible_python_interpreter=/usr/bin/python3

</code></pre>

<pre><code>
#group name developer, we can add multiple address
[developer]
192.168.21.129
</code></pre>

Some time only adding entry into host file doesn't work so add command into /etc/ansible/ansible.cfg
<pre><code>vim /etc/ansible/ansible.cfg</code></pre>
<pre><code>
[defaults]
inventory = /home/your_user/ansible/inventory
remote_user = ansible
</code></pre>

Command to check server and client is connected or not
<pre><code>ansible ping all -m ping -u ansible  #remote-user ansible</code></pre>
