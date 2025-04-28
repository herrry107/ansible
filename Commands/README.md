**Basic Ansible ad-hoc command**

<pre><code>ansible all --list-hosts #show all client machine</code></pre>
<pre><code>
ansible developer --list-hosts      #show all ips of developer group
ansible developer[0] --list-hosts   #we can see by indexing also
ansible developer[-1] --list-hosts  #reverse indexing
</code></pre>

**There are 3 ways to push code on node by server**
1) Adhoc Command (Linux Command, No Idempotency)
2) Modules (Single Work)
3) Playbooks (More than one module, YAML)

***1) Adhoc Command:*** 
- Ad-hoc commands are commands which can be run individually to perform quick functions.
- These ad-hoc commands are not used for configuration management and deployment because these command are of one time usage.
- The ansible ad-hoc commands uses the /usr/bin/ansible commands line tool to automate a single task

<pre><code>ansible developer -a "ls" -u ansible #-a means arguments</code></pre>
<pre><code>ansible developer -a "touch file" -u ansible #create file on node</code></pre>
<pre><code>ansible developer -a "sudo apt-get install nginx -y" -u ansible  #install package on node</code></pre>
<pre><code>ansible developer -ba "apt remove nginx -y" -u ansible   #-b means become super user like sudo</code></pre>
**-a: arguments**

**-b: become sudo**

**-u: run by user**

***2) Ansible Modules:***
- Ansible ships with a number of modules (Called Module Library) that can be executed directly on remote hosts or through 'playbook'.
- Your library of modules can reside on any machine, and there are no servers, daemons or database required.
- The default location for the inventory file is /etc/ansible/hosts

<pre><code>
#install package command for redhat-client
ansible developer -b -m yum -a "pkg=httpd state=present" -u ansible
#install package command for debian-client
ansible developer -b -m apt -a "pkg=apache2 state=present" -u ansible
</code></pre>

<pre><code>
#remove package
ansible developer -b -m apt -a "pkg=apache2 state=absent" -u ansible
</code></pre>

<pre><code>
#start service
ansible all -b -m service -a "name=apache2 state=started" -u ansibe
#stop service
ansible all -b -m service -a "name=apache2 state=stopped" -u ansible
</code></pre>

<pre><code>
#adding user to node
ansile all -b -m user -a "name=raj" -u ansible
</code></pre>

<pre><code>
#copy file onto remote
ansible all -b -m copy -a "src=file1.txt dest=/home/ansible" -u ansible
</code></pre>

<pre><code>
ansible demo -b -m setup -a "filter=*ipv4*"
</code></pre>

**-b: sudo user**

**-m: module-name**

**-a: pass argument**

***3) Ansible Playbook:***
- Playbook in ansible are written in YAML format.
- It is human readable data serialization language. It is commonly use for configuration files.
- Playbook is like a file where you write codes consists of **vars, tasks, handlers, files template and role**.
- Each playbook is composed of one or more 'modules' in a list modules is a collection of configuration file.
- Playbooks are divided into many sectors like
 
1) **Taskget Section:** Define the host against which playbooks task has to be executed.

2) **Variable Section:** Define Variable

3) **Task Section:** List of all modules that we need to run in an order. 

[Playbook](https://github.com/herrry107/ansible/tree/main/Commands/Playbook)
