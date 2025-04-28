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

for example 
<pre><code>
--- #A list of fruits
fruits:
    - Mango
    - Banana
    - Graps
    - Apply
</code></pre>
