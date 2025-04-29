**Ansible Vault**

**Ansible Vault allows keeping sensitive data such as passwords or keys in encrypted files, rather than a plaintext in your playbooks**

creating a new encrypted playbook
<pre><code>ansible-vault create vault.yml</code></pre>

edit the ansible-vault encrypted playbook
<pre><code>ansible-vault edit vault.yml</code></pre>

to change password
<pre><code>ansible-vault rekey vault.yml</code></pre>

to encrypt an existing playbook
<pre><code>ansible-vault encrypt target.yml</code></pre>

to decrypt an encrypted playbook
<pre><code>ansible-vault decrypt target.yml</code></pre>

run vault encrypted playbook 
<pre><code>ansible-playbook vault.yml --ask-vault-pass</code></pre>
