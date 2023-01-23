# docker-


https://phoenixnap.com/kb/list-of-docker-commands-cheat-sheet



# How to use Docker and migrate your existing Apps to your Linux Server?
How to use Docker and migrate your existing Apps? We will cover all the cool advantages of containerization, and how to easily migrate and manage your existing services and apps into Docker Containers on your Linux Server!

We will use the free and open-source software Docker.


Project Homepage: https://www.docker.com/
Documentation: https://docs.docker.com/

Video: https://youtu.be/y0GGQ2F2tvs

## Prerequisites

- Linux Server running Ubuntu 20.04 LTS or newer

*You can still install Docker on a Linux Server that is not running Ubuntu, however, this may require different commands!*

## 1. Install Docker, and Docker-Compose

You can still install Docker on a Linux Server that is not running Ubuntu, however, this may require different commands!

### 1.1. Install Docker
```bash
sudo apt update

sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### 1.2. Check if Docker is installed correctly
```bash
sudo docker run hello-world
```

### 1.3. Install Docker-Compose

Download the latest version (in this case it is 1.25.5, this may change whenever you read this tutorial!)

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

### 1.4. Check if Docker-Compose is installed correctly
```bash
sudo docker-compose --version
```

### 1.5. (optional) Add your linux user to the `docker` group
```bash
sudo usermod -aG docker $USER
```

## 2. Docker Basics

### 2.1. Run a Docker Container

```bash
docker run hello-world
```

### 2.2. How to find Docker Images?

To get new applications, just visit the [official Docker Hub](https://hub.docker.com/). Because most vendors and communities maintain their own images, you will find Images for many applications there.

### 2.3. Expose Ports

Run a simple NGINX webserver.

```bash
docker run -p 80:80 -d nginx
```

### 2.4. Persistent Volumes

```bash
docker run -p 80:80 -v nginx_data:/var/www/html -d nginx
```

### 2.5. Migrate static files to a Docker Volume

Migrate a NGINX webserver to Docker.

```bash
sudo systemctl stop nginx

sudo systemctl disable nginx

docker run -p 80:80 -v /var/www/html:/var/www/html -d nginx
```

### 2.6. Migrate databases to a Docker Volume

Migrate a MySQL Server to Docker.

```bash
sudo systemctl stop mysql-server

sudo systemctl disable mysql-server

docker run -v /var/lib/mysql:/var/lib/mysql -d mysql
```

## 3. Set up Portainer

### 3.1. Create a new Docker Volume

```bash
docker volume create portainer_data
```

### 3.2. Launch Portainer

```bash
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```






# Docker
**Docker** is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called _containers_. The service has both free and premium tiers. The software that hosts the containers is called **Docker Engine**.

Project Homepage: [Home - Docker](https://www.docker.com/)
Documentation: [Docker Documentation | Docker Documentation](https://docs.docker.com/)

---
## Installation

One click installation script:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Run docker as non root user:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

Install Docker Engine : [Docker Engine](https://docs.docker.com/engine/install/)

---
## Build Images


---
## Docker CLI

**Run Containers**

COMMAND | DESCRIPTION
---|---
`docker run IMAGE` | Start a new container
`docker run --name CONTAINER IMAGE` | Start a new container and set a name
`docker run -p HOSTPORT:CONTAINERPORT IMAGE` | Start a new container with mapped ports
`docker run -P IMAGE` | Start a new container and map all ports

**Container Management:**

COMMAND | DESCRIPTION
---|---
`docker create IMAGE` | Create a new container
`docker start CONTAINER` | Start a container
`docker stop CONTAINER` | Graceful stop a container
`docker kill CONTAINER` | Kill (SIGKILL) a container
`docker restart CONTAINER` | Graceful stop and restart a container
`docker pause CONTAINER` | Suspend a container
`docker unpause CONTAINER` | Resume a container
`docker rm CONTAINER` | Destroy a container

**Container Bulk Management**

COMMAND | DESCRIPTION
---|---
`docker stop $(docker ps -q)` | To stop all the running containers
`docker stop $(docker ps -a -q)` | To stop all the stopped and running containers
`docker kill $(docker ps -q)` | To kill all the running containers
`docker kill $(docker ps -a -q)` | To kill all the stopped and running containers
`docker restart $(docker ps  -q)` | To restart all  running containers
`docker restart $(docker ps -a -q)` | To restart all the stopped and running containers
`docker rm $(docker ps  -q)` | To destroy all running containers
`docker rm $(docker ps -a -q)` | To destroy all the stopped and running containers
`docker pause $(docker ps  -q)` | To pause all  running containers
`docker pause $(docker ps -a -q)` | To pause all the stopped and running containers
`docker start $(docker ps  -q)` | To start all  running containers
`docker start $(docker ps -a -q)` | To start all the stopped and running containers
`docker rm -vf $(docker ps -a -q)` | To delete all containers including its volumes use
`docker rmi -f $(docker images -a -q)` | To delete all the images
`docker system prune` | To delete all dangling and unused images, containers, cache and volumes
`docker system prune -a` | To delete all used and unused images
`docker system prune --volumes` | To delete all docker volumes

**Inspect Containers:**

COMMAND | DESCRIPTION
---|---
`docker ps` | List running containers
`docker ps -a` | List all containers, including stopped
`docker logs CONTAINER` | Show a container output
`docker logs -f CONTAINER` | Follow a container output
`docker top CONTAINER` | List the processes running in a container
`docker diff` | Show the differences with the image (modified files)
`docker inspect` | Show information of a container (json formatted)

**Run Commands:**

COMMAND | DESCRIPTION
---|---
`docker attach CONTAINER` | Attach to a container
`docker cp CONTAINER:PATH HOSTPATH` | Copy files from the container
`docker cp HOSTPATH CONTAINER:PATH` | Copy files into the container
`docker export CONTAINER` | Export the content of the container (tar archive)
`docker exec CONTAINER` | Run a command inside a container
`docker exec -it CONTAINER /bin/bash` | Open an interactive shell inside a container (there is no bash in some images, use /bin/sh)
`docker wait CONTAINER` | Wait until the container terminates and return the exit code

**Images:**

COMMAND | DESCRIPTION
---|---
`docker images` | List all local images
`docker history IMAGE` | Show the image history
`docker inspect IMAGE` | Show information (json formatted)
`docker tag IMAGE TAG` | Tag an image
`docker commit CONTAINER IMAGE` | Create an image (from a container)
`docker import URL` | Create an image (from a tarball)
`docker rmi IMAGE` | Delete images
`docker pull REPO:[TAG]` | pull an image/repo from a registry
`docker push REPO:[TAG]` | push and image/repo to a registry
`docker search TEXT` | Search an image on the official registry
`docker login` | Login to a registry
`docker logout` | Logout from a registry
`docker save REPO:[TAG]` | Export an image/repo as a tarball
`docker load` | Load images from a tarball

**Volumes:**

COMMAND | DESCRIPTION
---|---
`docker volume ls` | List all vol1umes
`docker volume create VOLUME` | Create a volume
`docker volume inspect VOLUME` | Show information (json formatted)
`docker volume rm VOLUME` | Destroy a volume
`docker volume ls --filter="dangling=true"` | List all dangling volumes (not referenced by any container)
`docker volume prune` | Delete all volumes (not referenced by any container)

### Backup a container
Backup docker data from inside container volumes and package it in a tarball archive.
`docker run --rm --volumes-from CONTAINER -v $(pwd):/backup busybox tar cvfz /backup/backup.tar CONTAINERPATH`

An automated backup can be done also by this [Ansible playbook](https://github.com/thedatabaseme/docker_backup).
The output is also a (compressed) tar. The playbook can also manage the backup retention.
So older backups will get deleted automatically.

To also create and backup the container configuration itself, you can use `docker-replay`for that. If you lose
the entire container, you can recreate it with the export from `docker-replay`.
A more detailed tutorial on how to use docker-replay can be found [here](https://thedatabaseme.de/2022/03/18/shorty-generate-docker-run-commands-using-docker-replay/).

### Restore container from backup
Restore the volume with a tarball archive.
`docker run --rm --volumes-from CONTAINER -v $(pwd):/backup busybox sh -c "cd CONTAINERPATH && tar xvf /backup/backup.tar --strip 1"`
## Networks

## Troubleshooting
### Networking
`docker run --name netshoot --rm -it nicolaka/netshoot /bin/bash`






#### Installing docker playbook Ansible 





---
- hosts: all
  
  become: yes
  tasks:

  # Install Docker
  # --
  # 
  - name: install prerequisites
    apt:
      name:
        - docker.io
      update_cache: yes

  - name: add user permissions
    shell: "usermod -aG docker {{ ansible_env.SUDO_USER }}"

  - name: Reset ssh connection for changes to take effect
    meta: "reset_connection"

  # Installs Docker SDK
  # --
  # 
  - name: install python package manager
    apt:
      name: python3-pip
  
  - name: install python sdk
    become_user: "{{ ansible_env.SUDO_USER }}"
    pip:
      name:
        - docker
        - docker-compose
