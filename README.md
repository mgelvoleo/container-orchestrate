# Container Orchestrate
This project will ochestrate the container by using docker swarm


# Step 1: provistion the workstation and server using vagrant note: Copy the Vagrantfile before lunching
```
vagrant up
```

# Step 2: Install the docker of each server, mind here i asume im using ansible for me to install both server in one playbook

## Step 2.1: 

sudo vim /etc/hosts

    192.168.56.10
    192.168.56.11
