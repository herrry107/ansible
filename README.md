**Ansible is an opensource IT configuration Management, Deployment and Orchestration tool. It aims to provide large productivity gains to a wide variety of automation challenges.**

**Ansible History**
- Michacl Denaan developed ansible and the ansible project begin in februray 2012
- Redhat acquired the ansible tool in 2015.
- Ansible is available for RHEL, Debian, Centos, Oracle Linux.

Ansible turns our code into infrastructure i.e. our computing environment has some of the same attributes as your application.
**IAC: Infrastructure as Code**

- Ansible is agent less like no client installation (like chef-client), direct ssh.
- Ansible playbook written in YAML (Yet Another Markup Language).

![Alt-text](https://github.com/herrry107/ansible/blob/main/images/ansible-architecture.png)

**Ansible Advantage**
1) Ansible is free to use by everyone.
2) Ansible is very consistent, light weight and no constraints regarding the OS or underlying hardware one present.
3) It is very secure due to its agentless capabilities and open SSH security features.
4) Ansible does not need any special system administrator skills to install and use it.
5) Push Mechanism.

**Ansible Disadvantage**
1) Insufficient user interface, though ansible tower is GUI, but it is still in development stages.
2) Cannot achieve full automation by ansible.
3) New to the market, therefore limited support and documentation is available.

**Term used in Ansible**
1) ***Ansible Server:*** The machine where ansible is installed and from which all tasks and playbook will be ran.
2) ***Module:*** Basically a module is a command or set of similar commands meant to be executed on the client-side.
3) ***Task:*** A task is a section that contain of a single proceduce to be completed.
4) ***Role:*** A way of organising tasks and related files to be later called in a playbook.
5) ***Fact:*** Information fetched from the client system from the global variables with the gather-facts operations.
6) ***Inventory:*** File containing data about the client-server.
7) ***Play:*** Execute of a playbook.
8) ***Handler:*** Task which is called only if a notifier is present.
9) ***Notifier:*** Section attributes to a task which calls a handler if the output is changed.
10) ***Playbook:*** It Contains code in YAML format. which describes tasks to be executed.
11) ***Host:*** Nodes which are automated by ansible.

-------------------------------------------------------------------------------------------------------

**Read All Docker Docs by these sequence**

- [1. Server-Client Configuration](https://github.com/herrry107/ansible/tree/main/Server-Client-Configuration)
- [2. Hosts](https://github.com/herrry107/ansible/tree/main/hosts)
- [3. Commands](https://github.com/herrry107/ansible/tree/main/Commands)
