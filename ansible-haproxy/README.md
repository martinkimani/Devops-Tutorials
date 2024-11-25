# Deploy and configure Haproxy with ansible in Debian

This script installs haproxy, configures it as a reverse proxy and configures ssl for your domains in debian and ubuntu 

## Pre-requisites
- install ansible in your local machine
- A user with sudo privileges in the remote server
- copy your local machines ssh public key to your remote server in the above

## Run

ansible-playbook vm-haproxy-playbook.yml -i inventory/inventory_haproxy.yml --user=appuser  --private-key ~/.ssh/id_rsa  --ask-become-pass --extra-vars "domain_ip=YOUR_DOMAIN_IP"

## partial Run
you can run parts of your ansible script using tags. you can tag a block of tasks or a single task.
e.g in the example below haparoxy is already installed and configured however we want to configure new sub-domains mapped to that ip, ssl and reverse proxying we only need to execute the tasks in the gen-certs and haproxy blocks as below.

ansible-playbook vm-haproxy-playbook.yml -i inventory/inventory_haproxy.yml --user=appuser  --private-key ~/.ssh/id_rsa  --ask-become-pass --extra-vars "domain_ip=YOUR_DOMAIN_IP" --tags gen-certs,haproxy

when you run the commands above it will as for the ask-become-pass that is the password of the sudo privileged user in your remote server.