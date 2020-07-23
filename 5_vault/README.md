ansible-vault encrypt /home/ansible/secret

echo "<pass>" > /home/ansible/vault

ansible-playbook --vault-password-file /home/ansible/vault /home/ansible/secPage.yml

curl -u bond http://node1/secure/classified.html



