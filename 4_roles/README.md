Create a Role Called baseline in /etc/ansible/roles.. this is present in our folder /etc

Create the structure needed for the role:

cd /etc/ansible/roles/
sudo mkdir baseline && sudo chown ansible.ansible /etc/ansible/roles/baseline
mkdir /etc/ansible/roles/baseline/{templates,tasks,files}
echo "---" > baseline/tasks/main.yml


cp /home/ansible/resources/motd.j2 baseline/templates

cat > baseline/tasks/deploy_motd.yml

---
- template:
    src: motd.j2
    dest: /etc/motd

ctrl+c

cat > baseline/tasks/deploy_nagios.yml

---
- yum: name=nrpe state=latest

ctrl+c

cat >  baseline/tasks/edit_hosts.yml

---
- lineinfile:
    line: "{{ ansible_default_ipv4.address }} nagios.example.com" 
    path: /etc/hosts

ctrl+c

cp /home/ansible/resources/authorized_keys /etc/ansible/roles/baseline/files/

cat > baseline/tasks/deploy_noc_user.yml

---
- user: name=noc
- file:
     state: directory
     path: /home/noc/.ssh
     mode: 0600
     owner: noc
     group: noc
- copy:
     src: authorized_keys
     dest: /home/noc/.ssh/authorized_keys
     mode: 0600
     owner: noc
     group: noc

ctrl+c


Change back to the home directory:

cd /home/ansible/

cat > resources/web.yml

---
- hosts: webservers
  become: yes
  roles:
    - baseline
  tasks:
    - name: install httpd
      yum: name=httpd state=latest
    - name: start and enable httpd
      service: name=httpd state=started enabled=yes
ctrl+c



ansible-playbook resources/web.yml

ssh node1
We should see a new MOTD, so we know that play worked.

See if the noc user was set up:

id noc
Check to see if the nrpe package was installed:

sudo yum list nrpe
