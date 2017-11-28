# atomicoind #

### Ansible playbook for provisioning EC2 hosts ###


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
