**Ansible Roles**

- We can use two techniques for reusing a set of tasks: include and roles
- Roles are good for organising tasks and encapsulating data needed to acomplish those tasks.

![Alt-text](https://github.com/herrry107/ansible/blob/main/images/ansible-roles.png)

- We can organise playbooks into a directory structure called roles.
- Adding more & more functionality to the playbooks will make it difficult to maintain in a single file.

1) **Default:** It stores the data about role/application default variables example: if you want to run to port 80 or 8080 then variables needs to define in this ports.

2) **Files:** It contains file need to be transferred to the remote VM(static files)

3) **Handlers:** They are triggers or task. We can segregate all the handlers required in playbook.

4) **Meta:** This directory contains files that establish roles dependencies example: Author name, Supported Platform, Dependencies if any.

5) **Tasks:** It contain all the tasks that is normally in the playbook example: Installing packages and copies files etc.

6) **Vars:** Variables for the role can be specified in this directory and used in your configuration files both vars and defaults stores variables.

create test-role
<pre><code>ansible-galaxy role init test-role</code></pre>

test-role.yml
<pre><code>
--- #handlers
- hosts: developer
  user: ansible
  become: yes
  roles:
    - test-role
</code></pre>

<pre><code>ansible-playbook test-role.yml</code></pre>

we have to put all thing like tasks, handlers vars in separate file in roleslike.

ansible/Roles/test-role/tasks/main.yml
<pre><code>
#SPDX-License-Identifier: MIT-0
---
# tasks file for test-role
- name: first install apache2
  action: apt name='{{pkgname}}' state=present
  notify: service installed #notify name and handler name must same
</code></pre>

ansible/Roles/test-role/vars/main.yml
<pre><code>
#SPDX-License-Identifier: MIT-0
---
# vars file for test-role
pkgname: apachei2
</code></pre>

ansible/Roles/test-role/handlers/main.yml
<pre><code>
#SPDX-License-Identifier: MIT-0
---
# handlers file for test-role
- name: service installed   #notify name and handler name must same
  action: service name='{{pkgname}}' state=restarted
</code></pre>
