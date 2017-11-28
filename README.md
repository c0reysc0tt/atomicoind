# atomicoind #

### An Ansible playbook for provisioning CentOS Atomic Host EC2 instances and installing Bitcoin in a container ###

Notes:
---------------------
This playbook includes two roles.  The first one provisions new CentOS Atomic Host instances. The second one installs a Docker container with Bitcoin Core installed.


To run:
---------------------
1. Copy and edit *vars/ec2.yml* with appropriate values for your AWS account. 
```bash 
   cp vars/ec2.yml vars/ec2.yml.bak
   vi vars/ec2.yml
```   

2. Run the atomicoind playbook
```bash
    ansible-playbook -b atomicoind.yml
```    

The Bitcoin container can be found here: https://hub.docker.com/r/c0reysc0tt/mybitcoind/
