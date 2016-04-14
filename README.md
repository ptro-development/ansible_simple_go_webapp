# ansible_simple_go_webapp
Ansible configuration for deployment of simple web application in writen Go language

*******************************
Description:
*******************************

This document describes how to set up Go simple application by executing Ansible modules:
- application_nodes
- web_nodes


*******************************
Requirements before deployment:
*******************************

- ansible was configured on all nodes to be able to execute playbooks agains them
-- ansible user created
-- ssh-keys generated and propagated
-- sudo set for ansible user to be able to run command as root
- the web Centos_6 available to run Nginx
-- name: master
- the application Centos_6 servers available to run simple go application
-- names:
--- client001 & client001
- source code of application ready under /home/ansible/simple_app.go


****************************************
Ansible hosts file at /etc/ansible/hosts
****************************************
Look at provided hosts file.

***************************************
Installation of application nodes
***************************************

cd /home/ansible/sainsbury_simple_go_webapp/roles
nsible-playbook application_nodes.yml


***************************************
Installation of web node server
***************************************

cd /home/ansible/sainsbury_simple_go_webapp/roles
ansible-playbook web_nodes.yml


***************************************
Testing

Note: Testing is also done as a part of
      web_nodes deployment.
***************************************

{code}
[ansible@master roles]$ for try in `seq 1 4`; do curl http://master/; echo; done
Hi there, I'm served from client002!
Hi there, I'm served from client001!
Hi there, I'm served from client002!
Hi there, I'm served from client001!
{code}
