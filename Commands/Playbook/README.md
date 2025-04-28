**An Ansible Playbook is a YAML file (.yml or .yaml) that describes a series of tasks to automate things like:**

- Installing software

- Configuring servers

- Managing users

- Setting up networks

- Deploying applications

- And much more

**YAML (Yet Another Markup Language)**
- For ansible, nearly every yaml files starts with a list.
- Each item in the list is a list of key-value pairs commonly called a dictonary.
- All YAML files have to begin with "---" and end with "..." but end mark not compulsory.
- All member of list lines must begin with same indentation level starting with "-"
- Extension of yaml is .yml or .yaml.

for example 
<pre><code>
--- #A list of fruits
fruits:
    - Mango
    - Banana
    - Graps
    - Apply
</code></pre>

A dictonary is represented in a simple key:value pair form.
for example
<pre><code>
--- #Details of Customer
Customer:
    name: Rajput
    job: Devops
    age: 25
</code></pre>

playbook1.yml
<pre><code>
--- #Gather info playbook
- hosts: developer    #target group
  user: ansible       #remote user run on node
  become: yes         # be or run with sudo
  connection: ssh
  gather_facts: yes
</code></pre>
<pre><code>ansible-playbook playbook1.yml</code></pre>

playbook2-apache.yml
<pre><code>
--- #install apache2 on node ubuntu
- hosts: developer
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: Install apache2 on ubuntu by ansible user
      action: apt name=apache2 state=present          #for redhat use yum
</code></pre>
<pre><code>ansible-playbook playbook2-apache.yml</code></pre>


-----------------------------------------------------------------------------

**Ansible Variable:** To use multiple location on script put variable section above tasks so that we define it first and use it later.

<pre><code>
--- #script for variable
- hosts: all
  user: ansible
  become: yes
  connection: ssh
  vars:
    pkgname: apache2
  tasks:
    - name: Remove apache2 from node 
      action: apt name='{{pkgname}}' state=absent
</code></pre>
<pre><code>ansible-playbook playbook3-variable.yml</code></pre>

----------------------------------------------------------------------------

**Ansible Handlers:** A handler is exactly the same as a task, but it will run when called by another task.

Handlers are just like regular tasks in an ansible playbook, but are only run if the task contains a notify direction and also indicates that is changed something.

playbook4-handler.yml
<pre><code>
--- #handlers
- hosts: developer
  user: ansible
  become: yes
  vars:
    pkgname: apache2
  tasks:
    - name: first install apache2
      action: apt name='{{pkgname}}' state=present
      notify: service installed #notify name and handler name must same
  handlers:
    - name: service installed   #notify name and handler name must same
      action: service name='{{pkgname}}' state=restarted
</code></pre>
<pre><code>ansible-playook playbook4-handler.yml
