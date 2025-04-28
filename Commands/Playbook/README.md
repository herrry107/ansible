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

