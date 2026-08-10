# Docker Basic Commands Cheat Sheet

Docker is a platform used to build, package, and run applications in
**containers**.

## 1. Docker Basic Concepts

  Term             Meaning
  ---------------- ------------------------------------------------
  Docker           Platform for containerization
  Image            Read-only blueprint used to create containers
  Container        Running instance of a Docker image
  Dockerfile       File containing instructions to build an image
  Docker Hub       Public registry for Docker images
  Volume           Persistent storage for containers
  Network          Communication system between containers
  Docker Compose   Tool for managing multiple containers

### Docker Workflow

``` text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

------------------------------------------------------------------------

# 2. Check Docker Installation

### Check Docker version

``` bash
docker --version
```

### Display detailed Docker information

``` bash
docker info
```

### Display Docker help

``` bash
docker help
```

------------------------------------------------------------------------

# 3. Docker Images

Images are templates used to create containers.

### List images

``` bash
docker images
```

or:

``` bash
docker image ls
```

### Download an image

``` bash
docker pull ubuntu
```

Example:

``` bash
docker pull python
```

### Inspect an image

``` bash
docker image inspect ubuntu
```

### Remove an image

``` bash
docker rmi ubuntu
```

### Remove unused images

``` bash
docker image prune
```

------------------------------------------------------------------------

# 4. Docker Containers

A container is a running instance of an image.

### Create and run a container

``` bash
docker run ubuntu
```

### Run interactively

``` bash
docker run -it ubuntu
```

### Open Ubuntu shell

``` bash
docker run -it ubuntu /bin/bash
```

### Run in background

``` bash
docker run -d ubuntu
```

`-d` means detached mode.

### Give a container a name

``` bash
docker run --name mycontainer ubuntu
```

### Run with port mapping

``` bash
docker run -p 8080:80 nginx
```

Meaning:

``` text
Host Port 8080 → Container Port 80
```

------------------------------------------------------------------------

# 5. List Containers

### Show running containers

``` bash
docker ps
```

### Show all containers

``` bash
docker ps -a
```

------------------------------------------------------------------------

# 6. Start, Stop and Restart Containers

### Start

``` bash
docker start mycontainer
```

### Stop

``` bash
docker stop mycontainer
```

### Restart

``` bash
docker restart mycontainer
```

### Pause

``` bash
docker pause mycontainer
```

### Unpause

``` bash
docker unpause mycontainer
```

------------------------------------------------------------------------

# 7. Remove Containers

### Remove a stopped container

``` bash
docker rm mycontainer
```

### Force remove a container

``` bash
docker rm -f mycontainer
```

### Remove all stopped containers

``` bash
docker container prune
```

------------------------------------------------------------------------

# 8. Execute Commands Inside a Container

### Open Bash shell

``` bash
docker exec -it mycontainer /bin/bash
```

If Bash is not available:

``` bash
docker exec -it mycontainer /bin/sh
```

### Execute a command

``` bash
docker exec mycontainer ls
```

Example:

``` bash
docker exec mycontainer pwd
```

------------------------------------------------------------------------

# 9. Container Logs

### View logs

``` bash
docker logs mycontainer
```

### Follow logs continuously

``` bash
docker logs -f mycontainer
```

### Show last 50 lines

``` bash
docker logs --tail 50 mycontainer
```

------------------------------------------------------------------------

# 10. Container Information

### Inspect a container

``` bash
docker inspect mycontainer
```

### Show resource usage

``` bash
docker stats
```

### Show processes inside a container

``` bash
docker top mycontainer
```

### Show port mappings

``` bash
docker port mycontainer
```

------------------------------------------------------------------------

# 11. Copy Files

### Copy file from host to container

``` bash
docker cp file.txt mycontainer:/file.txt
```

### Copy file from container to host

``` bash
docker cp mycontainer:/file.txt .
```

------------------------------------------------------------------------

# 12. Docker Volumes

Volumes provide persistent storage for containers.

### List volumes

``` bash
docker volume ls
```

### Create a volume

``` bash
docker volume create myvolume
```

### Inspect a volume

``` bash
docker volume inspect myvolume
```

### Remove a volume

``` bash
docker volume rm myvolume
```

### Mount a volume

``` bash
docker run -v myvolume:/data ubuntu
```

------------------------------------------------------------------------

# 13. Docker Networks

### List networks

``` bash
docker network ls
```

### Create a network

``` bash
docker network create mynetwork
```

### Inspect a network

``` bash
docker network inspect mynetwork
```

### Connect a container to a network

``` bash
docker network connect mynetwork mycontainer
```

### Disconnect a container

``` bash
docker network disconnect mynetwork mycontainer
```

### Remove a network

``` bash
docker network rm mynetwork
```

------------------------------------------------------------------------

# 14. Dockerfile

A `Dockerfile` contains instructions for building a Docker image.

Example:

``` dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

### Important Dockerfile instructions

  Instruction    Purpose
  -------------- -------------------------------------------
  `FROM`         Specifies the base image
  `WORKDIR`      Sets the working directory
  `COPY`         Copies files into the image
  `ADD`          Copies files and can handle archives/URLs
  `RUN`          Executes commands while building
  `EXPOSE`       Documents the container port
  `CMD`          Default command when the container starts
  `ENTRYPOINT`   Defines the main executable
  `ENV`          Sets environment variables

------------------------------------------------------------------------

# 15. Build Docker Image

Build an image from a Dockerfile:

``` bash
docker build -t myapp .
```

Explanation:

``` text
docker build    → Build image
-t myapp        → Give image a name
.               → Use current directory as build context
```

### List the image

``` bash
docker images
```

### Run the image

``` bash
docker run myapp
```

------------------------------------------------------------------------

# 16. Docker Compose

Docker Compose is used to define and run multiple containers.

A typical file is:

``` text
compose.yaml
```

or:

``` text
docker-compose.yml
```

### Start services

``` bash
docker compose up
```

### Start in background

``` bash
docker compose up -d
```

### Stop and remove services

``` bash
docker compose down
```

### Build services

``` bash
docker compose build
```

### Show services

``` bash
docker compose ps
```

### View logs

``` bash
docker compose logs
```

### Follow logs

``` bash
docker compose logs -f
```

------------------------------------------------------------------------

# 17. Docker Registry / Docker Hub

### Login

``` bash
docker login
```

### Tag an image

``` bash
docker tag myapp username/myapp:latest
```

### Push an image

``` bash
docker push username/myapp:latest
```

### Pull an image

``` bash
docker pull username/myapp:latest
```

------------------------------------------------------------------------

# 18. Docker Cleanup

### Remove unused containers

``` bash
docker container prune
```

### Remove unused images

``` bash
docker image prune
```

### Remove unused volumes

``` bash
docker volume prune
```

### Remove unused networks

``` bash
docker network prune
```

### Remove unused Docker resources

``` bash
docker system prune
```

### Remove unused resources including unused images

``` bash
docker system prune -a
```

> **Warning:** `docker system prune -a` can remove unused images and
> other resources. Use it carefully.

------------------------------------------------------------------------

# 19. Most Important Commands

These are the commands beginners should learn first:

  Command                            Purpose
  ---------------------------------- ----------------------------
  `docker --version`                 Check Docker version
  `docker pull image`                Download an image
  `docker images`                    List images
  `docker run image`                 Create and run a container
  `docker ps`                        List running containers
  `docker ps -a`                     List all containers
  `docker start container`           Start a container
  `docker stop container`            Stop a container
  `docker restart container`         Restart a container
  `docker rm container`              Remove a container
  `docker rmi image`                 Remove an image
  `docker exec -it container bash`   Enter a container
  `docker logs container`            View container logs
  `docker inspect container`         View detailed information
  `docker build -t name .`           Build an image
  `docker compose up`                Start Compose services
  `docker compose down`              Stop Compose services

------------------------------------------------------------------------

# 20. Practical Example

## Step 1: Pull Nginx

``` bash
docker pull nginx
```

## Step 2: Run Nginx

``` bash
docker run -d --name mynginx -p 8080:80 nginx
```

## Step 3: Check the container

``` bash
docker ps
```

## Step 4: Check logs

``` bash
docker logs mynginx
```

## Step 5: Stop the container

``` bash
docker stop mynginx
```

## Step 6: Start it again

``` bash
docker start mynginx
```

## Step 7: Remove the container

``` bash
docker rm mynginx
```

------------------------------------------------------------------------

# 21. Common Docker Options

  Option     Meaning
  ---------- ---------------------------------------------------
  `-d`       Detached/background mode
  `-it`      Interactive terminal
  `-p`       Port mapping
  `--name`   Assign container name
  `-v`       Mount a volume
  `-e`       Set environment variable
  `--rm`     Automatically remove container after it stops
  `-f`       Force operation
  `-t`       Assign a tag/name
  `-a`       Include all/unused resources depending on command

Example:

``` bash
docker run -d --name web -p 8080:80 nginx
```

This means:

``` text
-d              → Run in background
--name web      → Container name = web
-p 8080:80      → Map host port 8080 to container port 80
nginx           → Image
```

------------------------------------------------------------------------

# 22. Quick Revision

``` text
IMAGE
  ↓
docker pull
  ↓
IMAGE STORED LOCALLY
  ↓
docker run
  ↓
CONTAINER
  ↓
docker ps
  ↓
docker exec / logs / stats
  ↓
docker stop
  ↓
docker start
  ↓
docker rm
```

## Golden Rules

1.  **Image = Blueprint**
2.  **Container = Running instance of an image**
3.  **Dockerfile = Instructions to build an image**
4.  **Volume = Persistent data**
5.  **Network = Container communication**
6.  **Compose = Multiple-container management**
7.  `docker ps` → Check running containers
8.  `docker images` → Check images
9.  `docker logs` → Check application output
10. `docker exec` → Execute commands inside a container

------------------------------------------------------------------------

## Useful Command Pattern

``` bash
docker <command> <object> [options]
```

Examples:

``` bash
docker run nginx
docker stop mycontainer
docker rm mycontainer
docker images
docker ps -a
docker logs mycontainer
docker exec -it mycontainer /bin/bash
```
