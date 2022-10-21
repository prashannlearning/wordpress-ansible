# wordpress-ansible

<img width="1095" alt="image" src="https://user-images.githubusercontent.com/116376587/197271284-1e684ceb-4ef7-4709-b8f6-476bd933ef60.png">

We will see how to configure wordpress using ansible-playbook.

Pre-requisites:
  1. A server running with Ansible installed and configured act as control node, if not few quick setps
      a. yum install python3.9
      b. python3 -m pip install --user ansible
  2. A remote server which will be used as application server to configure wordpress.
  3. Control node and application node has ssh connectivity.

Assumptions:
1. Ec2 instance is up and running.
2. passwordless authentication is there between control and application node.

Considerations and Improvements for future:
1. To store DB password we can use ansible-vault.

Overview:
This ansible-playbook will install and configure wordpress on ec2 instance, it contains few sub plabooks and one main plabook which will do below things.

1. Install and configure apache httpd server with ssl enabled.
2. Install php and required modules.
3. Install and configure mysql db.
4. Download and configure wordpress bundle.
5. configure firewalld and open custom https port 8443.

Steps:
1. clone the repo to you control node.
2. cd wordpress-playbook
3. ansible-playbook playbook.yml -i hosts
