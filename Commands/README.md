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

