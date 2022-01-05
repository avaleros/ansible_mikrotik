# Ansible for Mikrotik
## Install Ansible

tested On Ubuntu 18.04

`sudo apt update`

`sudo apt install software-properties-common`

`sudo add-apt-repository --yes --update ppa:ansible/ansible`

`sudo apt install ansible`

## Install aditionals packages:

`sudo apt install python2-pip python3-pip`
`sudo pip install paramiko`

## Create user on Ubuntu

`sudo adduser ansible`

## Create ssh key
`ssh-keygen -t rsa -b 2048 -m PEM`

## Create user on Mikrotik

`/user add name=ansible password=**** group=full disabled=no`

Then, we need to import the public key to Mikrotik on /system/users

## Edit /etc/ansible/hosts file
Now, we need to add our mikrotik devices. Create a list [*here*] and add the ipaddress of devices.
Add variables. I prefed create one variable for each list created.
We need:

[*list*:vars]
ansible_user = ansible
ansible_network_os = routeros
ansible_connection = network_cli
ansible_port=*22*
gather_factes=false

Save and exit from file.

## Create the playbook
Create a file.yml with the name of the task. You can git my personal tasks.

## Run it!
`ansible-playbook -i hosts Mikrotik_Backup.yml -vvv`
