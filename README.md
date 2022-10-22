# wordpress-ansible

<img width="1095" alt="image" src="https://user-images.githubusercontent.com/116376587/197271284-1e684ceb-4ef7-4709-b8f6-476bd933ef60.png">

We will see how to configure wordpress using ansible-playbook.

# Pre-requisites:
  1. A server running with Ansible installed and configured act as control node, if not few quick setps
 
      a. yum install python3.9
      
      b. python3 -m pip install --user ansible
  2. A remote server which will be used as application server to configure wordpress.
  3. Control node and application node has ssh connectivity.

# Assumptions:
1. Ec2 instance is up and running.
2. passwordless authentication is there between control and application node.

# Considerations and Improvements for future:
1. To store DB password we can use ansible-vault.

# Overview:
This ansible-playbook will install and configure wordpress on ec2 instance, it contains few sub plabooks and one main plabook which will do below things.

1. Install and configure apache httpd server with ssl enabled.
2. Install php and required modules.
3. Install and configure mysql db.
4. Download and configure wordpress bundle.
5. configure firewalld and open custom https port 8443.

# Steps:
1. clone the repo to you control node.
2. cd wordpress-ansible
3. ansible-playbook playbook.yml -i hosts

X------------------------X--------------------------X---------------------------X-----------------------X

<img width="1226" alt="image" src="https://user-images.githubusercontent.com/116376587/197271989-13b877a0-a864-405f-850d-78c8e6ae8ca5.png">

# Making Wordpress highly available 

# Ansible Documentaion: 
https://docs.ansible.com/ansible/latest/collections/community/aws/elb_target_module.html

To make our wordpress site highly available we would need below services, assuming AWS as cloud provider.

1. Create launch configuration.
2. Application Load Balancer.
3. Target Group.
4. Autoscalling Group.

# Assumptions:
1. Control node can authenticate with aws in order to provision or configure service.
2. Above mentioned applications are already provisioned.

# Overview:
1. We will create a Launch configuration using an existing ec2 instance.
2. We will create TG for wp site.
3. We will create a ALB with listeners forwarding request to wp_tg when request comes to /wordpress.
4. we wiil create ASG with LB attached with mim 1 and desire 2 instance.


Steps:
1. cd HA_configuration
2. ansible-playbook playbook.yml -i ../hosts


# Dockerfile

<img width="1314" alt="image" src="https://user-images.githubusercontent.com/116376587/197334736-622158bc-0353-4e9f-9a76-6e9a6bba1cf6.png">

steps:

1. locate Dockerfile.
2. build docker image 
  docker build . -t wordpress
