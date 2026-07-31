# Docker

Docker is a platform for developing, shipping, and running applications inside lightweight, isolated containers.

> [!NOTE]
> Docker packages an application together with its dependencies into a **container**, ensuring that it runs consistently across different environments.

---

# 1. Docker Architecture

Docker consists of several core components.

| Component | Description |
|-----------|-------------|
| Docker Engine | The service responsible for building and running containers. |
| Docker Client | The `docker` command-line interface used to communicate with the Docker Engine. |
| Docker Daemon (`dockerd`) | Background service that manages images, containers, networks, and volumes. |
| Docker Image | A read-only template used to create containers. |
| Docker Container | A running instance of an image. |
| Docker Registry | Repository for storing and distributing images (e.g. Docker Hub). |

> [!IMPORTANT]
> An **image** is a template, while a **container** is a running instance of that image.

---

# 2. Docker Installation Verification

Verify that Docker is installed and running.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker version` | `docker version` | Displays Docker client and server versions. |
| `docker info` | `docker info` | Displays Docker system information. |
| `docker context ls` | `docker context ls` | Lists available Docker contexts. |
| `docker system info` | `docker system info` | Displays detailed Docker information (newer versions may recommend `docker info`). |


---

# 3. Docker Help

Display available commands and command-specific help.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker` | `docker` | Lists all Docker commands. |
| `docker help` | `docker help` | Displays general help. |
| `docker <command> --help` | `docker run --help` | Displays help for a specific command. |

Example:

```bash
docker run --help
```

---

# 4. Building Images

Docker images are built from a **Dockerfile**, which contains a sequence of instructions executed during the build process.

## Build Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker build` | `docker build <path/context>` | Build an image from a Dockerfile. |
| `docker build -t` | `docker build -t <image>:<tag> <path/context>` | Build an image with a name and tag. |
| `docker build --no-cache` | `docker build --no-cache <path/context>` | Build without using the cache. |
| `docker build -f` | `docker build -f <Dockerfile> <path/context>` | Use a custom Dockerfile. |

Example:

```bash
docker build -t myapp .
docker build -t myapp:1.0 .
```

Using a custom Dockerfile:

```bash
docker build -f Dockerfile.dev -t myapp:dev .
```

> [!IMPORTANT]
> The final argument (`.`) specifies the **build context**. Docker can only access files located inside this directory.


---

# 5. Images

Docker images are read-only templates used to create containers.

## Image Management

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker pull` | `docker pull <image>` | Download an image from a registry. |
| `docker images` | `docker images` | List local images. |
| `docker image ls` | `docker image ls` | List local images. |
| `docker image inspect` | `docker image inspect <image>` | Display detailed image information. |
| `docker rmi` | `docker rmi <image>` | Remove an image. |
| `docker image rm` | `docker image rm <image>` | Remove an image. |

Example:

```bash
docker pull nginx
docker images
docker image inspect nginx
```

> [!TIP]
> Docker automatically downloads an image the first time you run a container if it is not available locally.

---

# 6. Containers

Containers are isolated runtime instances created from Docker images.

## Container Lifecycle

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker run` | `docker run <image>` | Create and start a new container. |
| `docker create` | `docker create <image>` | Create a container without starting it. |
| `docker start` | `docker start <container>` | Start an existing container. |
| `docker stop` | `docker stop <container>` | Stop a running container gracefully. |
| `docker restart` | `docker restart <container>` | Restart a container. |
| `docker kill` | `docker kill <container>` | Forcefully stop a container. |
| `docker pause` | `docker pause <container>` | Pause all processes inside a container. |
| `docker unpause` | `docker unpause <container>` | Resume a paused container. |
| `docker rm` | `docker rm <container>` | Remove a stopped container. |

---

## Listing Containers

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker ps` | `docker ps` | List running containers. |
| `docker ps -a` | `docker ps -a` | List all containers. |
| `docker container ls` | `docker container ls` | List running containers. |
| `docker container ls -a` | `docker container ls -a` | List all containers. |

Example:

```bash
docker ps
docker ps -a
```

---

# 7. Running Containers

## Syntax

```bash
docker run [OPTIONS] IMAGE [COMMAND]
```

## Common Options

| Option | Description |
|---------|-------------|
| `-d` | Run container in detached mode. |
| `-it` | Interactive terminal. |
| `--name` | Assign a custom container name. |
| `--rm` | Automatically remove the container after it exits. |
| `-p` | Publish container ports. |
| `-e` | Set environment variables. |
| `-v` | Mount a volume or bind mount. |
| `--hostname` | Set the container hostname. |

Examples:

Run Ubuntu interactively:

```bash
docker run -it ubuntu bash
```

Run Nginx in the background:

```bash
docker run -d --name web nginx
```

Publish port 80:

```bash
docker run -d -p 8080:80 nginx
```

Automatically remove the container:

```bash
docker run --rm alpine echo "Hello Docker"
```

> [!IMPORTANT]
> `docker run` creates a **new container** every time it is executed.

> [!TIP]
> If you want to start an existing container, use `docker start` instead of `docker run`.

---

# 8. Container Information

Inspect running containers.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker inspect` | `docker inspect <container>` | Display detailed container information. |
| `docker logs` | `docker logs <container>` | Show container logs. |
| `docker logs -f` | `docker logs -f <container>` | Follow log output in real time. |
| `docker top` | `docker top <container>` | Show running processes. |
| `docker stats` | `docker stats` | Display live resource usage. |

Example:

```bash
docker logs nginx
docker logs -f nginx
docker stats
```

---

# 9. Executing Commands Inside Containers

Run commands inside running containers.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker exec` | `docker exec <container> <command>` | Execute a command. |
| `docker exec -it` | `docker exec -it <container> bash` | Open an interactive shell. |
| `docker attach` | `docker attach <container>` | Attach to the main container process. |

Example:

```bash
docker exec -it nginx bash
```

> [!NOTE]
> `docker exec` starts a **new process** inside the container, while `docker attach` connects to the container's primary process.

---

# 10. Removing Containers and Images

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker rm` | `docker rm <container>` | Remove a stopped container. |
| `docker rm -f` | `docker rm -f <container>` | Forcefully remove a running container. |
| `docker rmi` | `docker rmi <image>` | Remove an image. |
| `docker image prune` | `docker image prune` | Remove unused images. |
| `docker container prune` | `docker container prune` | Remove stopped containers. |

> [!WARNING]
> Removing an image that is still used by one or more containers will fail unless those containers are removed first.

---


# 11. Dockerfile

A **Dockerfile** is a text file containing instructions used to build Docker images.

## Build Process

```
Dockerfile
     │
     ▼
docker build
     │
     ▼
Docker Image
     │
     ▼
docker run
     │
     ▼
Container
```

> [!NOTE]
> Docker executes Dockerfile instructions from top to bottom. Each instruction creates a new image layer unless stated otherwise.

---

## Common Dockerfile Instructions

| Instruction | Syntax | Description |
|-------------|--------|-------------|
| `FROM` | `FROM <image>` | Specify the base image(OS). |
| `RUN` | `RUN <command>` | Execute a command during image build(install dependencies for ex.). |
| `COPY` | `COPY <src> <dest>` | Copy files into the image(Usualy copy all with "COPY . /app"). |
| `ADD` | `ADD <src> <dest>` | Copy files or extract archives. |
| `WORKDIR` | `WORKDIR <path>` | Set the working directory. |
| `ENV` | `ENV KEY=value` | Set environment variables. |
| `ARG` | `ARG NAME=value` | Define build-time variables. |
| `EXPOSE` | `EXPOSE <port>` | Document the listening port. |
| `USER` | `USER <user>` | Set the default user. |
| `VOLUME` | `VOLUME ["/data"]` | Define a mount point. |
| `CMD` | `CMD ["command"]` | Default command executed when the container starts(For example: ./main ). |
| `ENTRYPOINT` | `ENTRYPOINT ["command"]` | Configure the container executable. |
| `HEALTHCHECK` | `HEALTHCHECK ...` | Configure container health checks. |
| `LABEL` | `LABEL key=value` | Add image metadata. |

---

# 12. Sample Dockerfile

```dockerfile
FROM ubuntu:24.04

LABEL version="1.0"

WORKDIR /app

COPY . /app

RUN apt update && \
    apt install -y python3

EXPOSE 8080

CMD ["python3","app.py"]
```

---

# 13. Image Tagging

Docker tags uniquely identify image versions.

## Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker tag` | `docker tag <image> <new-image>` | Create a new tag for an existing image. |
| `docker image tag` | `docker image tag <image> <new-image>` | Equivalent command. |

Example

```bash
docker tag myapp:latest myapp:v1.0
```

---

# 14. Saving and Loading Images

Transfer images between systems without using a registry.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker save` | `docker save -o <file.tar> <image>` | Save an image as a tar archive. |
| `docker load` | `docker load -i <file.tar>` | Load an image from a tar archive. |

Example

```bash
docker save -o nginx.tar nginx
docker load -i nginx.tar
```

---

# 15. Importing and Exporting Containers

Export or import an entire container filesystem.

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker export` | `docker export <container> > file.tar` | Export a container filesystem. |
| `docker import` | `docker import <file.tar> <image>` | Create an image from an exported filesystem. |

Example

```bash
docker export my-container > backup.tar
docker import backup.tar restored-image
```

> [!NOTE]
> `docker save/load` preserves image metadata and layers, while `docker export/import` only transfers the container filesystem.

# 16. Docker Volumes

Volumes provide persistent storage independent of a container's lifecycle.

> [!IMPORTANT]
> Data stored inside a container is lost when the container is removed unless it is stored in a **volume** or **bind mount**.

---

## Volume Types

| Type | Description |
|------|-------------|
| Named Volume | Managed by Docker and stored in Docker's data directory. |
| Anonymous Volume | Automatically created without a specific name. |
| Bind Mount | Maps a host directory into the container. |
| tmpfs Mount | Stores data only in memory. |

---

## Volume Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker volume create` | `docker volume create <name>` | Create a new volume. |
| `docker volume ls` | `docker volume ls` | List volumes. |
| `docker volume inspect` | `docker volume inspect <volume>` | Show volume details. |
| `docker volume rm` | `docker volume rm <volume>` | Remove a volume. |
| `docker volume prune` | `docker volume prune` | Remove unused volumes. |

Example

```bash
docker volume create mysql-data

docker volume ls
```

---

## Mounting a Volume

```bash
docker run -v mysql-data:/var/lib/mysql mysql
```

or

```bash
docker run --mount source=mysql-data,target=/var/lib/mysql mysql
```

---

## Bind Mounts

Bind mounts connect a directory from the host machine to a directory inside the container.

Syntax

```bash
docker run -v <host-path>:<container-path> <image>
```

Example

```bash
docker run -v $(pwd):/app ubuntu
```

Windows

```powershell
docker run -v C:\Projects\App:/app ubuntu
```

> [!TIP]
> Bind mounts are commonly used during development so changes made on the host are immediately visible inside the container.

---

# 17. Docker Networks

Docker networks enable communication between containers.

---

## Network Drivers

| Driver | Description |
|--------|-------------|
| `bridge` | Default network for containers on a single host. |
| `host` | Container shares the host's network stack. |
| `none` | No networking. |
| `overlay` | Connects containers across multiple Docker hosts. |
| `macvlan` | Assigns a MAC address directly to the container. |

---

## Network Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker network ls` | `docker network ls` | List networks. |
| `docker network inspect` | `docker network inspect <network>` | Display network details. |
| `docker network create` | `docker network create <name>` | Create a network. |
| `docker network rm` | `docker network rm <network>` | Remove a network. |
| `docker network prune` | `docker network prune` | Remove unused networks. |
| `docker network connect` | `docker network connect <network> <container>` | Connect a container to a network. |
| `docker network disconnect` | `docker network disconnect <network> <container>` | Disconnect a container from a network. |

Example

```bash
docker network create backend
```

---

## Port Mapping

Expose a container port to the host.

Syntax

```bash
docker run -p <host-port>:<container-port> <image>
```

Example

```bash
docker run -p 8080:80 nginx
```

Multiple ports

```bash
docker run \
-p 8080:80 \
-p 8443:443 \
nginx
```

> [!NOTE]
> Without port mapping, services running inside a container are generally not accessible from the host.

---

# 18. Docker Compose

Docker Compose simplifies running multi-container applications.

> [!IMPORTANT]
> Docker Compose uses a YAML file (`compose.yaml` or `docker-compose.yml`) to define services, networks, and volumes.

---

## Common Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker compose up` | `docker compose up` | Create and start services. |
| `docker compose up -d` | `docker compose up -d` | Run services in detached mode. |
| `docker compose down` | `docker compose down` | Stop and remove services. |
| `docker compose start` | `docker compose start` | Start existing services. |
| `docker compose stop` | `docker compose stop` | Stop running services. |
| `docker compose restart` | `docker compose restart` | Restart services. |
| `docker compose ps` | `docker compose ps` | List services. |
| `docker compose logs` | `docker compose logs` | Show service logs. |
| `docker compose exec` | `docker compose exec <service> bash` | Open a shell inside a service. |
| `docker compose pull` | `docker compose pull` | Download service images. |
| `docker compose build` | `docker compose build` | Build service images. |

---

## Compose File Structure

```yaml
services:
  web:
  database:

networks:

volumes:
```

---

## Minimal Example

```yaml
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"
```

Start

```bash
docker compose up
```

Stop

```bash
docker compose down
```

---

## Common Compose Properties

| Property | Description |
|-----------|-------------|
| `image` | Image to use. |
| `build` | Docker build context. |
| `container_name` | Custom container name. |
| `ports` | Publish ports. |
| `volumes` | Mount volumes. |
| `environment` | Environment variables. |
| `depends_on` | Service dependencies. |
| `networks` | Networks used by the service. |
| `restart` | Restart policy. |
| `command` | Override the default command. |

Example

```yaml
services:
  app:
    image: nginx
    container_name: web
    restart: always
    ports:
      - "8080:80"
```

---

# 19. Docker Registry

A Docker registry stores and distributes Docker images.

---

## Common Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker login` | `docker login` | Authenticate with a registry. |
| `docker logout` | `docker logout` | Log out of a registry. |
| `docker push` | `docker push <image>` | Upload an image. |
| `docker pull` | `docker pull <image>` | Download an image. |
| `docker search` | `docker search <name>` | Search Docker Hub. |

Example

```bash
docker login

docker push username/myapp:1.0
```

---

## Tag Before Pushing

```bash
docker tag myapp username/myapp:1.0
docker push username/myapp:1.0
```

> [!TIP]
> Images must be tagged with your registry namespace before they can be pushed to Docker Hub or another registry.

---

# 20. Environment Variables

Environment variables allow configuration without modifying the application.

Run a container

```bash
docker run -e APP_ENV=production nginx
```

Multiple variables

```bash
docker run \
-e USER=admin \
-e PASSWORD=secret \
myapp
```

Environment file

```bash
docker run --env-file .env myapp
```

Example `.env`

```text
DB_HOST=mysql
DB_PORT=3306
APP_ENV=production
```

> [!NOTE]
> Environment variables are commonly used for configuration but should not be used to store sensitive production secrets.

# 21. Docker System Management

Manage Docker resources and reclaim disk space.

## System Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker system df` | `docker system df` | Display Docker disk usage. |
| `docker system prune` | `docker system prune` | Remove unused Docker resources. |
| `docker system prune -a` | `docker system prune -a` | Remove all unused images and resources. |
| `docker system info` | `docker system info` | Display detailed Docker system information. |
| `docker system events` | `docker system events` | Stream Docker events in real time. |

Example

```bash
docker system df
```

Remove unused resources

```bash
docker system prune
```

> [!WARNING]
> `docker system prune -a` removes all unused images, containers, networks, and build cache. Ensure no important resources are needed before running it.

---

# 22. Monitoring and Troubleshooting

Inspect containers and diagnose common issues.

## Monitoring Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker logs` | `docker logs <container>` | Display container logs. |
| `docker logs -f` | `docker logs -f <container>` | Follow log output. |
| `docker inspect` | `docker inspect <container>` | Display detailed configuration. |
| `docker top` | `docker top <container>` | Show running processes. |
| `docker stats` | `docker stats` | Display live resource usage. |
| `docker diff` | `docker diff <container>` | Show filesystem changes. |
| `docker events` | `docker events` | Display Docker daemon events. |

Example

```bash
docker logs web
docker inspect web
docker stats
```

---

## Common Troubleshooting Workflow

1. Verify that the container is running.

```bash
docker ps
```

2. Review container logs.

```bash
docker logs <container>
```

3. Inspect container configuration.

```bash
docker inspect <container>
```

4. Open a shell inside the container.

```bash
docker exec -it <container> bash
```

5. Check resource usage.

```bash
docker stats
```

> [!TIP]
> Most Docker issues can be diagnosed using `docker ps`, `docker logs`, and `docker inspect`.

---

# 23. Docker Cleanup

Remove unused Docker resources.

## Cleanup Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `docker container prune` | `docker container prune` | Remove stopped containers. |
| `docker image prune` | `docker image prune` | Remove dangling images. |
| `docker image prune -a` | `docker image prune -a` | Remove all unused images. |
| `docker volume prune` | `docker volume prune` | Remove unused volumes. |
| `docker network prune` | `docker network prune` | Remove unused networks. |
| `docker builder prune` | `docker builder prune` | Remove build cache. |
| `docker system prune` | `docker system prune` | Remove unused resources. |

Example

```bash
docker image prune
docker volume prune
docker system prune
```

---

# 24. Best Practices

> [!IMPORTANT]
> Follow these practices when building and deploying Docker containers.

- Use **official base images** whenever possible.
- Keep images as small as possible.
- Use **specific image tags** instead of `latest`.
- Minimize the number of image layers.
- Store persistent data in **volumes**, not inside containers.
- Use `.dockerignore` to exclude unnecessary files.
- Run containers as a **non-root user** whenever possible.
- Keep secrets outside Dockerfiles and images.
- Use multi-stage builds to reduce image size.
- Remove unused Docker resources periodically.

---

# 25. Common Docker Workflow

```
Write Dockerfile
        │
        ▼
docker build
        │
        ▼
Docker Image
        │
        ▼
docker run
        │
        ▼
Container
        │
        ├──────────────┐
        ▼              │
 docker logs           │
 docker exec           │
 docker inspect        │
 docker stats          │
        │              │
        ▼              │
docker stop            │
        │              │
        ▼              │
 docker rm ◄───────────┘
```

---

# 26. Command Reference

| Category | Common Commands |
|-----------|-----------------|
| Images | `docker pull` `docker build` `docker images` `docker tag` `docker push` |
| Containers | `docker run` `docker ps` `docker stop` `docker start` `docker restart` `docker rm` |
| Container Access | `docker exec` `docker attach` `docker logs` `docker inspect` |
| Volumes | `docker volume create` `docker volume ls` `docker volume rm` |
| Networks | `docker network create` `docker network ls` `docker network connect` |
| Compose | `docker compose up` `docker compose down` `docker compose build` `docker compose logs` |
| Registry | `docker login` `docker push` `docker pull` |
| Cleanup | `docker system prune` `docker image prune` `docker volume prune` |
| Monitoring | `docker stats` `docker top` `docker diff` `docker events` |

---

# 27. Docker CLI Cheat Syntax

The general syntax for Docker commands is:

```bash
docker <object> <command> [OPTIONS]
```

Examples

```bash
docker image ls
docker container ls
docker volume ls
docker network ls
docker compose up
```

Many Docker commands also have shorter aliases.

| Full Command | Alias |
|--------------|-------|
| `docker image ls` | `docker images` |
| `docker container ls` | `docker ps` |
| `docker container rm` | `docker rm` |
| `docker image rm` | `docker rmi` |

> [!NOTE]
> Docker provides both the newer object-oriented syntax (`docker image ls`) and the traditional shorthand syntax (`docker images`). Both forms are valid.

---

# 28. Exit Codes

Docker commands return exit codes indicating success or failure.

| Exit Code | Meaning |
|-----------|---------|
| `0` | Command completed successfully. |
| Non-zero | An error occurred. |
| `125` | Docker daemon or CLI error. |
| `126` | Command found but cannot be executed. |
| `127` | Command not found inside the container. |

Example

```bash
docker run alpine unknown-command
```

---

# 29. Useful References

| Resource | Description |
|----------|-------------|
| Docker Documentation | Official Docker documentation. |
| Docker Hub | Public registry for Docker images. |
| Docker Compose Specification | Compose file reference. |

