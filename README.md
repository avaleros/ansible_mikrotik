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

## Create user on Mikrotik

`/user add name=ansible password=**** group=full disabled=no`

## Create ssh key
`ssh-keygen -t rsa -b 2048 -m PEM`

Then, we need to import the key to Mikrotik on /system/users

