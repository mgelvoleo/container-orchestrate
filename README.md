# Container Orchestrate
This project will ochestrate the container by using docker swarm


# Step 1: provistion the workstation and server using vagrant note: Copy the Vagrantfile before lunching
```
vagrant up
```

# Step 2: Install the docker of each server, mind here i asume im using ansible for me to install both server in one playbook

## Step 2.1: 

sudo vim /etc/hosts

    192.168.56.10  srv1
    192.168.56.11  srv2

## Step 2.2:

ssh-keygen
ssh-copy-id localhost && ssh-copy-id srv1 && ssh-copy-id srv2

## Step 2.3:
sudo apt update
sudo apt install ansible

## Step 2.3
ansible all -m ping


##Step 2.4: 
ansible-playbook -i inventory -K install_docker.yml


# Step 3: Let move foreward on docker

alias stopdockers='sudo docker stop $(docker ps -a -q)'

alias docker='sudo docker'

alias rmdockers='sudo docker rm $(docker ps -a -q)'


docker images ls


docker images

 docker run -it ubuntu:22.04
 docker ps -a

Detach mode
docker run -it -d ubuntu:22.04

 docker exec 9a17f51c1ad6 hostname
 
 Attach Mode
 docker attach infallible_herschel
 
 
 docker search nginx
 
 
 docker commit 1f0b7f3f8465 ubuntu:python
 
 docker image rm nginx:latest
 
