1) Two Instances are created on AWS cloud using AWS console.

a) Get the AMI-Ubuntu-16.04
b) Select the VPN, Subnet
c) Create TAG's
d) Create a Security group's
e) Create the key and launch the two servers.
d) Give hostname as a MSR-test-Instance-1 and MSR-test-Instance-2.
# hostnamectl set-hostname MSR-test-Instance-1
# hostnamectl set-hostname MSR-test-Instance-2
Note: There is no Idea on Terraform, so I did manually. I am familiar with Cloud formation.


2) Installed Ansible on local machine.
a) configure the host file.
# vi /etc/ansible/hosts
# [MSR-servers]
# Client1 ansible_ssh_host=IP-1
# Client2 ansible_ssh_host=IP-2
b) Configure the SSH keys. We had to copy the ssh-public keys to authorized_keys files and try to login to host machines.
# ssh ubuntu@Host-IP
c) To check the connection between the hosts
# ansible -m ping all
# ansible -m ping MSR-servers
d) Written play-book for docker and docker-compose installation. Please check the file at https://github.com/raoavula/MSR-test
# ansible-playbook docker.yml
e) Written another play-book for installation for node and npm. Please the files at https://github.com/raoavula/MSR-test
# ansible-playbook node.yml


3) Docker container creation on MSR-test-Instance-1
a)  In previous, we already installed the docker and docker-compose through ansible. 
b) login to the MSR-test-Instance-1 through ssh using git bash/putty
c) create a directory structure for docker.
# mkdir apache-webserver
# mkdir webhtml
# vi Dockerfile (to get the html file from git hub)
d) go back to the apache-webserver directory
# cd apache-webserver
# vi docker-compose.yml
e) run the docker-compose file.
# docker-compose -p apache-webserver up --build -d
Note: Please refer the files at mentioned location https://github.com/raoavula/MSR-test


4) Docker container creation on MSR-test-Instance-2
a) In previous, we already installed the docker and docker-compose through ansible. 
b) login to the MSR-test-Instance-1 through ssh using git bash/putty
c) create a directory structure for docker.
# mkdir CouchDB
# vi docker-compose.yml
# docker-compose -p CouchDB up --build -d
Note: Please refer the file at mentioned location https://github.com/raoavula/MSR-test
