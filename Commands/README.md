**Basic Ansible ad-hoc command**

<pre><code>ansible all --list-hosts #show all client machine</code></pre>
<pre><code>
ansible developer --list-hosts      #show all ips of developer group
ansible developer[0] --list-hosts   #we can see by indexing also
ansible developer[-1] --list-hosts  #reverse indexing
</code></pre>

