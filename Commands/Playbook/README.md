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
<pre><code>ansible-playook playbook4-handler.yml</code></pre>
![Alt-text](https://github.com/herrry107/ansible/blob/main/images/ansible-handler.png)

<pre><code>
#Check Whether the playbook is formatted correctly or not (dry-run)
ansible-playbook playbook4-handler.yml
</code></pre>

----------------------------------------------------------------------------

**copy files**

<pre><code>

--- #copy file from server to client
- hosts: developer
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: copy file from server to client
      copy:
        src: /home/pratik/ansible-practice/ansible/Commands/Playbook/test-script.sh
        dest: /home/ansible/
        owner: ansible   #owner of file in node
        mode: ugo=rw    #permission
        backup: yes     #create new file if last one already present
</code></pre>

----------------------------------------------------------------------------

**Run shell command**

<pre><code>

--- #run shell script on node
- hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: run shell script
      shell: /home/ansible/test-script.sh >> /home/ansible/log.txt
</code></pre>

<pre><code>

--- #run shell script on node
- hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: run shell script
      shell: echo "hello" >> /home/ansible/hello1.txt
</code></pre>

----------------------------------------------------------------------------

**Loops**

loops include changing ownership on several files and or directories with the file module, creating multiple users with the user module and repeating a polling step untill certain results is reached

playbook7-loops.yml
<pre><code>
--- #loops
- hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: add list of user in my nodes
      user: name='{{item}}' state=present
      with_items:
        - varun
        - amit
</code></pre>
<pre><code>ansible-playbook playbook7-loops.yml</code></pre>
<pre><code>

--- #loops
- hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: add list of user in my nodes
      user: name='{{item}}' state=absent
      with_items:
        - varun
        - amit
</code></pre>

----------------------------------------------------------------------------

**Conditions**

Whenever we have different scenarios we put conditions according to the scenario. Sometime we want to skip a particular command on a particular node.
**when** statement

playbook8-conditions.yml
<pre><code>
--- #conditional command
- hosts: developer
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: Install httpd in Redhat
      command: yum install httpd -y
      when: ansible_os_family=="RedHat"
    - name: Install apache2 in Debian
      command: apt-get install apache2 -y
      when: ansible_os_family=="Debian"
</code></pre>
<pre><code>ansible-playbook playbook8-conditions.yml</code></pre>

----------------------------------------------------------------------------

**USER**

playbook9-user-create.yml
<pre><code>
--- #user creation
- name: create user
  hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: User Creation
      user:
        name: nick
        comment: new user adding in team
        shell: /bin/bash
</code></pre>

playbook10-delete-user
<pre><code>
--- #user deletion
- name: delete user
  hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: User Deletion
      user:
        name: nick
        comment: new user adding in team
        shell: /bin/bash
        state: absent
        remove: yes
</code></pre>

----------------------------------------------------------------------------

**CREATE FILE & DIRECTORY**

playbook11-file-directory.yml
<pre><code>

--- #creating files and directory
- name: create file & directory
  hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: create file101.txt
      file:
        path: /home/ansible/file101.txt
        state: touch
        owner: ansible
        group: ansible
        mode: ugo=rw
    - name: create directory
      file:
        path: /home/ansible/dir1
        state: directory
</code></pre>

----------------------------------------------------------------------------

**manage service**

playbook12-service.yml
<pre><code>
--- #install nginx and start service
- name: start service
  hosts: developer
  user: ansible
  become: yes
  tasks:
    - name: install nginx
      apt:
        name: nginx
        state: present
      notify: nginx-installed
  handlers:    
    - name: nginx-installed
      service:
        name: nginx
        state: stopped
        enabled: no
</code></pre>

