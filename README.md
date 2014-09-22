This is an ansible repository for deployment of Caliopen infrastructure.

Deployment is done using [ansible](www.ansible.com) playbooks.

2 types of deployments are possibles:

- single machine deployment
- 2 distincts machines set, one for web application another for backend services



# Installation

if ansible is not installed on your system:
- make a virtualenv, activate it
- pip -r requirements.txt

# Configuration

## x509 configuration

- Edit certificates information using your own (rsa key are
crypted inside this repository they will not work for you)

```
rm roles/web/files/certs/*
# generate a new key and csr
openssl req -new -newkey rsa:2048 \
    -keyout roles/web/files/certs/caliopen.key \
    -out roles/web/files/certs/caliopen.crt

# generate the certificate using [CaCert](www.cacert.org) for example
# and set this certificate as roles/web/file/certs/caliopen.crt file
```

## Ansible configuration
- Edit a hosts file with a webservers and backends groups and
  reachable address of related machines

- Edit a group_vars/backends file using backend.tmpl template
- Edit a group_var/webservers file using webservers.tmpl template
- Edit a host_vars/<machine_name> for all of your machines using relatedtemplate
  switch machine role

NOTE:

For deployment on a single machine, make the machine appear in
both webservers and backends groups

Set the private_ip_address in host_vars/<machine_name> to 127.0.0.1

For deployment on 2 distincts groups of machines, make sure you can have
a private network usable on eth1 interface for your machines. This kind of

# Deployment

## single machine deployment

```
ansible-playbook -i hosts single.yaml
```

## 2 groups of machines

```
ansible-playbook -i hosts backends.yaml
ansible-playbook -i hosts webservers.yaml
```

## Development environment

There's some special tasks for development (actually there is one that will generate a self-signed cert for you).  
You can activate it with following configuration:

```
#file: group_vars/webservers
is_dev_env: true
```

# Usage

Hence deployment is done, you can play with the caliopen cli command
on the webservers machines. You have to activate the python virtualenv
for that.

```
su - caliopen
source /var/projects/caliopen/env/bin/activate
```
