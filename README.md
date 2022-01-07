# Ansible for Mikrotik
## Install Ansible

tested on Ubuntu 18.04

`sudo apt update`

`sudo apt install software-properties-common`

`sudo add-apt-repository --yes --update ppa:ansible/ansible`

`sudo apt install python3 python3-pip ansible -y`

## Install aditionals packages:

`sudo pip3 install --upgrade pip`

`sudo pip3 install paramiko`

## Modify ansible.cnf
In the file **/etc/ansible/ansible.cfg** we will add the following line inside the [defaults] section to hide some errors in the execution of the Ansible playbook:
`deprecation_warnings=False`

Also we added another line to uncheck the host key ssh. If you don't do that you need to connect for first time at all Mikrotik devices by ssh: `host_key_checking=False`

## Create user on Ubuntu

`sudo adduser ansible`

## Create ssh key
`ssh-keygen -t rsa -b 2048 -m PEM`

## Create user on Mikrotik

`user add name=ansible password=*********** group=full comment="usuario ansible"`

`user ssh-keys import public-key-file=id_rsa.pub user=ansible`

`file remove id_rsa.pub`

## Edit /etc/ansible/hosts file
Now, we need to add our mikrotik devices. Create a list [*here*] and add the ipaddress of devices.
Add variables. I prefer create one variable for each list created.
We need:

[*list*:vars]

`ansible_user = ansible`

`ansible_network_os = routeros`

`ansible_connection = network_cli`

`ansible_port=*22*`

`gather_factes=false`

Save and exit from file.

## Create the playbook
`sudo mkdir /etc/ansible/tasks`

Create a file.yml with the name of the task. You can git my personal tasks.

## Run it!
`ansible-playbook -i hosts Mikrotik_Backup.yml -vvv`

## Add to crontab
`crontab -e`

Every sunday of every month at 03:59 am

`59 03 * * 0 /bin/ansible-playbook -i /etc/ansible/hosts /etc/ansible/tasks/Mikrotik_Backup.yml > /home/ansible/log_ansible.log 2>&`

## More
You can install playbooks comunnity:
`ansible-galaxy collection install community.routeros`
