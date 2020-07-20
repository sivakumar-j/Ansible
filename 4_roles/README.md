Create a Role Called baseline in /etc/ansible/roles.. this is present in our folder /etc

Create the structure needed for the role:

cd /etc/ansible/roles/
sudo mkdir baseline && sudo chown ansible.ansible /etc/ansible/roles/baseline
mkdir /etc/ansible/roles/baseline/{templates,tasks,files}
echo "---" > baseline/tasks/main.yml


cp /home/ansible/resources/motd.j2 baseline/templates

* cat > baseline/tasks/deploy_motd.yml
* cat > baseline/tasks/deploy_nagios.yml
* cat >  baseline/tasks/edit_hosts.yml
* cp /home/ansible/resources/authorized_keys /etc/ansible/roles/baseline/files/
* cat > baseline/tasks/deploy_noc_user.yml
* cat > baseline/tasks/main.yml
* cd /home/ansible/
* cat > resources/web.yml

ansible-playbook resources/web.yml
Check Our Work
Log in to one of the nodes (the IP addresses are on the hands-on lab overview page):

ssh node1
We should see a new MOTD, so we know that play worked.

See if the noc user was set up:

id noc
Check to see if the nrpe package was installed:

sudo yum list nrpe
