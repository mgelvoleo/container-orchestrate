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


# Step 3: Let move foreward on docker Sample Command
```
Create alias
alias stopdockers='sudo docker stop $(docker ps -a -q)'

alias docker='sudo docker'

alias rmdockers='sudo docker rm $(docker ps -a -q)'
```

```
docker images ls
```

```
docker images
```

```
 docker run -it ubuntu:22.04
 docker ps -a
```

```
Detach mode
docker run -it -d ubuntu:22.04
```

```
docker exec 9a17f51c1ad6 hostname
```
```
 Attach Mode
 docker attach infallible_herschel
``` 
 
``` 
 docker search nginx
``` 
 
 ```
 docker commit 1f0b7f3f8465 ubuntu:python
 ```
 
```
docker image rm nginx:latest
``` 

```
docker image inspect ubuntu:python-tree
``` 

``` 
docker exec 29ce1d99a43f ps -aux
```

```
docker run -d -it --name test1 -e MYSQL_PASSWORD='SecurePassword' ubuntu:22.04 bash
```

```
docker run -d --name web01 -h web01 -p 8000:80 nginx
```

```
docker restart web01
```

```
docker stop web01
docker start web01
docker logs web01
docker inspect c16394710b7b
docker inspect -f '{{.Config.Image}}' web01
```
```
docker network ls
```

```
docker network create frontend
docker network create backend
```
```
docker network connect frontend web01
```

```
docker network connect backend web01
```

```
docker network connect backend db1
```

```
docker network inspect backend
```

```
docker exec db1 apt-get update -y && docker exec db1 apt-get install iputils-ping -y
```
```
docker exec web01 ping db1
```

```
docker exec db1 apt install curl -y
```

```
docker run -d -it --network frontend --name proxy1 ubuntu:22.04
```

### Step 4: Create Dockerfile
```
FROM library/ubuntu:22.04


RUN apt update -y
RUN apt dist-upgrade -y
RUN apt install python3-pip -y
RUN pip3 install flask

ENV HOME /home

COPY flaskapp /home/flaskapp

EXPOSE 5000

STOPSIGNAL SIGTERM

WORKDIR /home/flaskapp

ENTRYPOINT ["python3"]

```


```
Bash Command
docker image build -t ubuntu:simple-flask .
```

```
docker history ubuntu:simple-flask
```

```
docker run -d --hostname webserver --name webserver -p 80:5000 ubuntu:simple-flask
```

## Create a Swarm
```
docker swarm init --advertise-addr 192.168.56.10
```

## Switch to our node2 or server2 to execute the following command of docker

```
Bash Command
docker swarm join --token SWMTKN-1-29miqz6havq2zlk5sx4lt3pphzi5rpuaol9bqnab7kacihwew3-5dp6kiemqhr33bkaes0ahpitc 192.168.56.10:2377
```


 
## Go back on our node 1, and create service try scale one of container
```
docker service create --replicas 1 --name pingdocker2 alpine  ping docker.com
```
