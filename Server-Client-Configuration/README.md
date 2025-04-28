**Create Server Machine First**

**Installation for UBUNTU Server**
<pre><code>
#update system
sudo apt update && sudo apt upgrade -y</code></pre>

<pre><code>
#install ansible
sudo apt install software-properties-common -y
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
</code></pre>
<pre><code>ansible --version</code></pre>

**Command for UBUNTU Server/Client**
<pre><code>sudo apt install openssh-client -y</code></pre>
<pre><code>
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
</code></pre>

**Installation for REDHAT Server**
<pre><code>
#using wget
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
yum install epel-release-latest-9.noarch.rpm
yum update -y
yum install ansible -y
</code></pre>

<pre><code>
#using dnf
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
yum update -y
yum install ansible -y
</code></pre>
