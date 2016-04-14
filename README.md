# ansible_simple_go_webapp
Ansible configuration for deployment of simple web application writen in Go language

# Description:
This document describes how to set up Go simple application by executing Ansible's modules on CentOS system:
- application_nodes
- web_nodes

# These are requirements to fullfil before deployment:
1. The web server available to run Nginx load balancer
 1. master

2. The application servers available to run simple web go application
 1. client001
 2. client002

3. Ansible was configured on all servers to be able to execute playbooks agains them
 1. an ansible user was created
 2. ssh keys were generated and propagated
 3. sudo was set for the ansible user to be able to run command as root
 4. ansible hosts file at /etc/ansible/hosts was provided
   * look at provided hosts file in main project directory

4. Source code of application is ready under /home/ansible/simple_app.go
 * code is available under application_code/simple_app.go

# Installation of application nodes
```
cd /home/ansible/ansible_simple_go_webapp/roles
ansible-playbook application_nodes.yml
```

# Installation of web server node
```
cd /home/ansible/ansible_simple_go_webapp/roles
ansible-playbook web_nodes.yml
```

# Testing
> Note: Testing is also done as a part of web_nodes deployment.
```
[ansible@master roles]$ for try in `seq 1 4`; do curl http://master/; echo; done
Hi there, I'm served from client002!
Hi there, I'm served from client001!
Hi there, I'm served from client002!
Hi there, I'm served from client001!
```
