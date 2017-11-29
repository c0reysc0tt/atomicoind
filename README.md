# atomicoind #

### An Ansible playbook that provisions CentOS Atomic Host EC2 instances and installs a Bitcoin container ###

Notes:
---------------------
This playbook includes two plays/roles.  The first one provisions new CentOS Atomic Host instances. The second one installs a Docker container with Bitcoin Core installed.


To run:
---------------------
1. Copy and edit *vars/ec2.yml* with appropriate values for your AWS account. 
```bash 
   cp vars/ec2.yml vars/ec2.yml.bak
   vi vars/ec2.yml
```   

2. Run the atomicoind playbook.
```bash
    ansible-playbook -b atomicoind.yml
```    
NOTE: If your private key isn't already included in your ansible config, you'll need to include it:
```bash
   ansible-playbook -vv -b atomicoind.yml --private-key=~/.ssh/my-key.pem
```

About the instance:
---------------------
This instance runs CentOS Atomic Host, which already has Docker installed, but sudo is required to run all docker commands by default.  For more info on this, see:
https://www.projectatomic.io/blog/2015/08/why-we-dont-let-non-root-users-run-docker-in-centos-fedora-or-rhel/

About the Container:
---------------------
The Docker image used to run the container is a proof of concept only. For space reasons, it doesn't mount a volume for the blockchain. It's based on Ubuntu:14.04 and Bitcoin Core has been compiled from scratch. Since we don't want to sync the entire blockchain, the container simply runs "test_bitcoin" and then stops.  You can see the results with:
```bash
   sudo docker logs -f mybitcoind
```
To run other commands, you can either start the container again and attach to it with a bash prompt while test_bitcoin is still running:
```bash
   sudo docker start mybitcoind
   sudo docker exec -i -t mybitcoind /bin/bash
```

...OR you can run a new container from the same image, like:
```bash
   sudo docker run --name mybitcoind2 -it c0reysc0tt/mybitcoind /bin/bash
```
From this prompt you can run commands such as 'bitcoind -version' to test the container.

The container can be found here: https://hub.docker.com/r/c0reysc0tt/mybitcoind/
