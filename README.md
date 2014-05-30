This is an ansible repository for deployment of Caliopen infrastructure.

2 groups of machine are managed at this time:

- webservers, using nginx to serve the wsgi application
- backends, using cassandra, elasticsearch, redis and rabbitmq as services.

a private network on eth1 is setup for all machines, and all backend services
bind only on the private ip address of this interface.

Deployment is mostly done on Gandi vm with a private vlan, so playbooks
are structured this way.


Installation:

if ansible is not installed on your system:
- make a virtualenv, activate it
- pip -r requirements.txt


- edit a hosts file with a webservers and backends groups and
  reachable address of related machines
- ansible-playbook -i hosts backends.yml, to deploy on backend machines
- ansible-playbook -i hosts webservers.yml, to deploy on web machines


Remarks:
- a x509 certificate and its private key are deployed on nginx.
  the private key in this repository is crypted of course. Replace
  the certificate and the key by your own (can be self signed)
  see roles/web/files/certs/ directory

- npm installation doesn't work very well, install manually if it's
  not working.

- web service startup is not correctly integrated in system. you'll
  find a pserve.sh file to startup the wsgi application.

- many things are in an early development step, so don't expect too
  much from these playbooks.
