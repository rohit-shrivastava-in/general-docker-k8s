# general-docker-k8s



# Docker Setup and Management Guide

## Verify Docker Installation

### Check Docker Version
```bash
docker --version
```

### Check Docker Status
```bash
systemctl status docker
```
> Press `q` to exit.

---

## Create and Manage Containers

### Run an Nginx Container (Detached Mode)
```bash
docker container run --publish 80:80 --detach nginx
```

### List Running Containers
```bash
docker ps
```

---

## Create a MySQL Container

### Run MySQL Container with Empty Password
```bash
docker container run -d -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql
```

### Access MySQL Container
```bash
docker exec -it <container_id> bash
```

### Log into MySQL
```bash
mysql -u root -p
```
> Press `Enter` for no password.

### Show Databases
```sql
show databases;
```

### Exit MySQL and Container
```bash
exit
exit
```

---

## Run a Container Without Detached Mode
```bash
docker container run --publish 82:80 nginx
```

---

## Manage MongoDB Container

### Run MongoDB Container
```bash
docker run --name mongo -d mongo
```

### Check MongoDB Container's Process
```bash
docker top mongo
```

### Find the Process ID
```bash
ps aux
```

### Kill the Process and Check Container Status
```bash
kill -9 <process_id>
docker ps -a
```

---

## Docker Networking

### List Running Containers
```bash
docker ps
```

### Inspect a Container
```bash
docker inspect <container_id>
```

### List Docker Networks
```bash
docker network ls
```

### Inspect Bridge Network
```bash
docker network inspect bridge
```

### Run a Container with Exposed Port (Ensure Unique Ports)
```bash
docker run -p 81:80 -d httpd
```

---

## Custom Network

### Create a Custom Network
```bash
docker network create myapp_network
```

### Run Containers in the Custom Network
```bash
docker run -d --name new_nginx --network myapp_network nginx:alpine
docker run -d --name old_nginx --network myapp_network nginx:alpine
```

### Verify Both Containers Are in the Same Network
```bash
docker network inspect myapp_network
```

### Test Container Communication
```bash
docker exec -it new_nginx curl old_nginx
docker exec -it old_nginx curl new_nginx
```

---

## Docker Volumes for MySQL

### Run MySQL Container with a Volume
```bash
docker container run -d --name db -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql-db:/var/lib/mysql mysql:9
```

### Access the Container and Check Databases
```bash
docker exec -it db bash
mysql -u root -p
```
> Press `Enter` for no password.

### Create a Database and List Databases
```sql
create database general;
show databases;
```

### Exit MySQL and Container
```bash
exit
exit
```

### Inspect the Docker Volume
```bash
docker volume ls
docker volume inspect mysql-db
```

### Check Data Directory on the Host Machine
```bash
cd /var/lib/docker/volumes/mysql-db/_data
ls
```
> You should see the `general` DB.

---

## Update the Container

### Stop and Remove the Old Container
```bash
docker stop db
docker rm db
```

### Run a New Version of MySQL Container with the Same Volume
```bash
docker container run -d --name db -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql-db:/var/lib/mysql mysql:9.0.1
```

### Verify the Container is Running
```bash
docker ps
```
