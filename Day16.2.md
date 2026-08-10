# Docker Concepts — Definitions and Syntax

A beginner-friendly Docker reference covering 15 important concepts.

---

# 1. Docker Architecture

## Definition

Docker Architecture describes how the major Docker components work together to build, run, store, and manage containers.

### Main Components

- **Docker Client** — Command-line interface used to send commands to Docker.
- **Docker Daemon** — Background service that manages images, containers, networks, and volumes.
- **Docker Host** — System where Docker Engine and containers run.
- **Docker Registry** — Repository used to store and distribute Docker images.
- **Docker Image** — Read-only template used to create containers.
- **Docker Container** — Running instance of an image.

## Syntax

```bash
docker <command> <object> [options]
```

## Example

```bash
docker run -d --name web nginx
```

### Architecture Flow

```text
Docker Client
      |
      v
Docker Daemon
      |
      +---- Docker Images
      |
      +---- Containers
      |
      +---- Networks
      |
      +---- Volumes
      |
      v
Docker Registry
```

---

# 2. Docker Images vs Containers

## Definition

### Docker Image

A Docker Image is a read-only template containing the application code, dependencies, libraries, and configuration required to create a container.

### Docker Container

A Docker Container is a running or stopped instance created from a Docker image.

## Image → Container

```text
Docker Image
     |
     | docker run
     v
Docker Container
```

## Syntax

```bash
docker pull <image>
docker run <image>
```

## Example

```bash
docker pull nginx
docker run -d --name mynginx nginx
```

## Difference

| Image | Container |
|---|---|
| Blueprint/template | Instance of image |
| Read-only | Has a writable container layer |
| Used to create containers | Runs the application |
| Can be shared through registries | Has a lifecycle |
| Created using Dockerfile/build | Created using `docker run` |

---

# 3. Dockerfile

## Definition

A Dockerfile is a text file containing instructions used to build a Docker image.

## Basic Syntax

```dockerfile
INSTRUCTION argument
```

## Important Dockerfile Instructions

### FROM

**Definition:** Specifies the base image.

**Syntax:**

```dockerfile
FROM <image>:<tag>
```

**Example:**

```dockerfile
FROM python:3.12
```

---

### RUN

**Definition:** Executes a command during image building.

**Syntax:**

```dockerfile
RUN <command>
```

**Example:**

```dockerfile
RUN pip install flask
```

---

### COPY

**Definition:** Copies files or directories from the build context into the image.

**Syntax:**

```dockerfile
COPY <source> <destination>
```

**Example:**

```dockerfile
COPY . /app
```

---

### CMD

**Definition:** Specifies the default command that runs when a container starts.

**Syntax:**

```dockerfile
CMD ["executable", "parameter"]
```

**Example:**

```dockerfile
CMD ["python", "app.py"]
```

---

### ENTRYPOINT

**Definition:** Configures the main executable of a container.

**Syntax:**

```dockerfile
ENTRYPOINT ["executable", "parameter"]
```

**Example:**

```dockerfile
ENTRYPOINT ["python"]
```

---

### WORKDIR

**Definition:** Sets the working directory for subsequent Dockerfile instructions.

**Syntax:**

```dockerfile
WORKDIR <path>
```

**Example:**

```dockerfile
WORKDIR /app
```

---

## Complete Dockerfile Example

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

## Build Image

```bash
docker build -t myapp .
```

## Run Container

```bash
docker run -p 5000:5000 myapp
```

---

# 4. Docker Volumes

## Definition

A Docker Volume is Docker-managed storage used to persist data independently of a container's writable layer.

If a container is removed, data stored in a volume can remain available.

## Create Volume

**Syntax:**

```bash
docker volume create <volume-name>
```

**Example:**

```bash
docker volume create myvolume
```

## List Volumes

```bash
docker volume ls
```

## Inspect Volume

```bash
docker volume inspect myvolume
```

## Mount Volume

**Syntax:**

```bash
docker run -v <volume-name>:<container-path> <image>
```

**Example:**

```bash
docker run -d -v myvolume:/data ubuntu
```

## Remove Volume

```bash
docker volume rm myvolume
```

---

# 5. Docker Networks

## Definition

A Docker Network allows containers and other Docker resources to communicate with each other.

Containers connected to the same user-defined network can generally communicate using container names.

## List Networks

```bash
docker network ls
```

## Create Network

**Syntax:**

```bash
docker network create <network-name>
```

**Example:**

```bash
docker network create mynetwork
```

## Run Container on Network

**Syntax:**

```bash
docker run --network <network-name> <image>
```

**Example:**

```bash
docker run -d --name web --network mynetwork nginx
```

## Connect Existing Container

```bash
docker network connect mynetwork mycontainer
```

## Disconnect Container

```bash
docker network disconnect mynetwork mycontainer
```

---

# 6. Docker Compose

## Definition

Docker Compose is a tool for defining and running multi-container applications using a YAML configuration file.

A Compose file is commonly named:

```text
compose.yaml
```

or:

```text
docker-compose.yml
```

## Basic Syntax

```yaml
services:
  service_name:
    image: image_name
    ports:
      - "host_port:container_port"
```

## Example

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  redis:
    image: redis
```

## Start Services

```bash
docker compose up
```

## Start in Background

```bash
docker compose up -d
```

## Stop and Remove Services

```bash
docker compose down
```

## Build Services

```bash
docker compose build
```

## Show Services

```bash
docker compose ps
```

## View Logs

```bash
docker compose logs
```

---

# 7. Docker Registry & Docker Hub

## Definition

A Docker Registry is a service that stores and distributes Docker images.

**Docker Hub** is a widely used public registry for Docker images.

## Login

```bash
docker login
```

## Pull Image

**Syntax:**

```bash
docker pull <repository>:<tag>
```

**Example:**

```bash
docker pull nginx:latest
```

## Tag Image

**Syntax:**

```bash
docker tag <local-image> <username>/<repository>:<tag>
```

**Example:**

```bash
docker tag myapp username/myapp:latest
```

## Push Image

```bash
docker push username/myapp:latest
```

## Pull Your Image

```bash
docker pull username/myapp:latest
```

---

# 8. Docker Ports & Port Mapping

## Definition

Port mapping connects a port on the Docker host to a port inside a container.

It allows applications running inside containers to be accessed from outside the container.

## Syntax

```bash
docker run -p <host-port>:<container-port> <image>
```

## Example

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host Port 8080
      |
      v
Container Port 80
      |
      v
Nginx
```

You can then access the application through the host's port 8080.

## Multiple Port Mappings

```bash
docker run -p 8080:80 -p 8443:443 nginx
```

---

# 9. Docker Environment Variables

## Definition

Environment variables are key-value configuration values passed to a container at runtime or defined in an image.

They are commonly used for application configuration such as ports, database names, and runtime settings.

## Syntax

```bash
docker run -e VARIABLE=value <image>
```

## Example

```bash
docker run -e APP_ENV=production myapp
```

## Multiple Variables

```bash
docker run -e APP_ENV=production -e PORT=5000 myapp
```

## Using an Environment File

**Syntax:**

```bash
docker run --env-file <file> <image>
```

**Example:**

```bash
docker run --env-file .env myapp
```

Example `.env`:

```text
APP_ENV=production
PORT=5000
```

> Do not put passwords, API keys, or other sensitive credentials into files that will be committed to a public repository.

---

# 10. Docker Container Lifecycle

## Definition

The Docker Container Lifecycle describes the different states and operations a container goes through from creation to removal.

## Lifecycle

```text
Image
  |
  v
docker create
  |
  v
Created
  |
  | docker start
  v
Running
  |
  +---- docker pause ----> Paused
  |                           |
  |<------ docker unpause ---+
  |
  | docker stop
  v
Stopped
  |
  | docker start
  +----------> Running
  |
  | docker rm
  v
Removed
```

## Create Container

```bash
docker create --name mycontainer nginx
```

## Start

```bash
docker start mycontainer
```

## Stop

```bash
docker stop mycontainer
```

## Restart

```bash
docker restart mycontainer
```

## Pause

```bash
docker pause mycontainer
```

## Unpause

```bash
docker unpause mycontainer
```

## Remove

```bash
docker rm mycontainer
```

---

# 11. Docker Bind Mounts vs Volumes

## Definition

Both bind mounts and volumes allow data to be stored outside a container's writable layer.

### Volume

A volume is managed by Docker and stored in Docker's storage area.

**Syntax:**

```bash
docker run -v <volume-name>:<container-path> <image>
```

**Example:**

```bash
docker run -v myvolume:/data ubuntu
```

### Bind Mount

A bind mount maps a specific host directory or file directly into a container.

**Syntax:**

```bash
docker run -v <host-path>:<container-path> <image>
```

**Example:**

```bash
docker run -v ./app:/app myapp
```

## Comparison

| Feature | Volume | Bind Mount |
|---|---|---|
| Managed by Docker | Yes | No |
| Host path required | No | Yes |
| Good for persistent application data | Yes | Yes |
| Useful for development | Yes | Very useful |
| Portability | Generally better | Depends on host path |

---

# 12. Docker Image Layers & Caching

## Definition

Docker images are built from layers. Many Dockerfile instructions create filesystem layers, and Docker can reuse unchanged build steps through its build cache.

This can make repeated builds faster.

## Example

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

Conceptually:

```text
Layer 1 → Base Python Image
Layer 2 → WORKDIR /app
Layer 3 → requirements.txt
Layer 4 → Installed dependencies
Layer 5 → Application code
Layer 6 → Runtime configuration
```

## Build Syntax

```bash
docker build -t <image-name> .
```

## Example

```bash
docker build -t myapp .
```

## Cache Concept

If an earlier build step has not changed, Docker may reuse its cached result.

### Good Practice

Copy dependency files before frequently changing source code:

```dockerfile
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
```

This can improve build-cache reuse when only application source files change.

---

# 13. Docker Security Basics

## Definition

Docker Security involves protecting images, containers, hosts, networks, secrets, and the Docker daemon from unauthorized access or malicious activity.

## Basic Security Practices

- Use trusted and minimal base images.
- Keep Docker and images updated.
- Avoid running applications as root when possible.
- Do not store secrets directly in Dockerfiles.
- Use `.dockerignore`.
- Limit container privileges.
- Expose only required ports.
- Scan images for vulnerabilities.
- Use read-only filesystems when appropriate.
- Use resource limits where appropriate.

## Run as a Non-root User

Dockerfile syntax:

```dockerfile
USER <username-or-uid>
```

Example:

```dockerfile
RUN useradd -m appuser
USER appuser
```

## Read-only Container Filesystem

```bash
docker run --read-only nginx
```

## Limit Memory

```bash
docker run --memory=512m nginx
```

## Limit CPU

```bash
docker run --cpus=1 nginx
```

> Security options depend on the application. Test restrictions before deploying to production.

---

# 14. Docker Multi-stage Builds

## Definition

A multi-stage Docker build uses multiple `FROM` stages in one Dockerfile. Build tools and intermediate files can remain in a builder stage while only the required runtime artifacts are copied into the final image.

This can produce smaller and cleaner production images.

## Syntax

```dockerfile
FROM <base-image> AS builder

# Build application

FROM <runtime-image>

COPY --from=builder <source> <destination>
```

## Example

```dockerfile
FROM node:22 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html
```

## Build

```bash
docker build -t myapp .
```

## Benefits

- Smaller final image
- Fewer unnecessary build tools
- Better separation between build and runtime
- Reduced attack surface

---

# 15. Docker in DevOps / CI-CD

## Definition

Docker in DevOps provides a consistent way to package applications and their dependencies into containers.

In CI/CD pipelines, Docker can be used to:

1. Build application images.
2. Test applications in isolated environments.
3. Push images to a registry.
4. Deploy images to development, staging, or production environments.

## Basic CI/CD Flow

```text
Developer
    |
    v
Git Repository
    |
    v
CI Pipeline
    |
    +---- Build
    |
    +---- Test
    |
    +---- Docker Image
    |
    v
Docker Registry
    |
    v
Deployment
    |
    v
Container
```

## Typical Commands

### Build

```bash
docker build -t myapp:latest .
```

### Run Tests

```bash
docker run --rm myapp:latest
```

### Tag

```bash
docker tag myapp:latest username/myapp:latest
```

### Push

```bash
docker push username/myapp:latest
```

### Pull on Deployment Server

```bash
docker pull username/myapp:latest
```

### Run

```bash
docker run -d --name myapp username/myapp:latest
```

---

# Quick Revision Table

| # | Concept | Main Purpose |
|---|---|---|
| 1 | Docker Architecture | Understand Docker components |
| 2 | Images vs Containers | Understand image-to-container workflow |
| 3 | Dockerfile | Build custom images |
| 4 | Volumes | Persist data |
| 5 | Networks | Connect containers |
| 6 | Docker Compose | Manage multiple containers |
| 7 | Registry & Docker Hub | Store/share images |
| 8 | Ports & Mapping | Access container applications |
| 9 | Environment Variables | Configure applications |
| 10 | Container Lifecycle | Manage container states |
| 11 | Bind Mounts vs Volumes | Manage external data |
| 12 | Layers & Caching | Understand image builds and optimization |
| 13 | Security | Protect Docker environments |
| 14 | Multi-stage Builds | Create smaller production images |
| 15 | DevOps / CI-CD | Build, test, publish, and deploy applications |

---

# Essential Docker Syntax Cheat Sheet

```bash
# Docker information
docker --version
docker info

# Images
docker pull <image>
docker images
docker rmi <image>

# Containers
docker run <image>
docker run -d --name <name> <image>
docker ps
docker ps -a
docker start <container>
docker stop <container>
docker restart <container>
docker rm <container>

# Execute commands
docker exec -it <container> /bin/bash

# Logs
docker logs <container>

# Build
docker build -t <image-name> .

# Ports
docker run -p <host-port>:<container-port> <image>

# Environment variables
docker run -e KEY=value <image>

# Volumes
docker volume create <volume>
docker volume ls
docker run -v <volume>:/data <image>

# Networks
docker network create <network>
docker network ls
docker run --network <network> <image>

# Compose
docker compose up
docker compose up -d
docker compose down

# Registry
docker login
docker tag <image> <username>/<repo>:<tag>
docker push <username>/<repo>:<tag>
docker pull <username>/<repo>:<tag>
```

---

# Summary

Docker provides a complete platform for containerizing applications.

The most important relationships are:

```text
Dockerfile
    |
    | docker build
    v
Docker Image
    |
    | docker run
    v
Docker Container
    |
    +---- Volume
    |
    +---- Network
    |
    +---- Port
    |
    +---- Environment Variables
```

For multi-container applications:

```text
Docker Compose
      |
      +---- Web Container
      |
      +---- Database Container
      |
      +---- Cache Container
```

For DevOps:

```text
Code
  ↓
Build
  ↓
Test
  ↓
Docker Image
  ↓
Registry
  ↓
Deploy
  ↓
Container
```
