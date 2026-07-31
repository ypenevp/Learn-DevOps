# Dockerfile

> [!NOTE]
> A Dockerfile is a text file containing a sequence of instructions used to build a Docker image.
> Each instruction creates a new image layer, resulting in a reproducible and portable environment.

---

# Table of Contents

- Dockerfile Overview
- Build Process
- Dockerfile Syntax
- Dockerfile Instructions
- Build Context
- Comments
- FROM
- RUN
- COPY
- ADD
- WORKDIR
- LABEL
- USER
- EXPOSE
- VOLUME
- ARG
- ENV
- CMD
- ENTRYPOINT
- HEALTHCHECK
- Multi-stage Builds
- .dockerignore
- Best Practices
- Instruction Reference

---

# Dockerfile Overview

A **Dockerfile** describes how a Docker image should be built.

The Docker engine reads the instructions **from top to bottom**, executing each instruction in order.

Typical workflow:

```text
Dockerfile
      │
docker build
      │
      ▼
Docker Image
      │
docker run
      ▼
Container
```

> [!IMPORTANT]
> Docker images are built **once**, while containers are **created and executed** from those images.

---

# Build Process

Build an image:

```bash
docker build -t myapp .
```

Run a container:

```bash
docker run myapp
```

Build and run workflow:

```text
Source Code
      │
Dockerfile
      │
docker build
      ▼
Docker Image
      │
docker run
      ▼
Container
```

---

# Dockerfile Syntax

A Dockerfile consists of one instruction per line.

General syntax:

```dockerfile
INSTRUCTION arguments
```

Example:

```dockerfile
FROM ubuntu:24.04

WORKDIR /app

COPY . .

RUN apt update

CMD ["bash"]
```

---

## Rules

- Instructions are executed **from top to bottom**.
- One instruction should be written per line.
- Instructions are **case-insensitive**, but are conventionally written in **uppercase**.
- Blank lines improve readability.
- Comments begin with `#`.

Example

```dockerfile
# Base image
FROM ubuntu

# Install packages
RUN apt update
```

> [!TIP]
> Writing instructions in uppercase improves readability and follows Docker's official conventions.

---

# Dockerfile Instructions

Docker provides a fixed set of instructions.

| Instruction | Purpose |
|-------------|---------|
| `FROM` | Specify the base image. |
| `RUN` | Execute commands during image build. |
| `COPY` | Copy files into the image. |
| `ADD` | Copy files and extract archives or download URLs. |
| `WORKDIR` | Set the working directory. |
| `LABEL` | Add metadata. |
| `USER` | Specify the user for subsequent instructions. |
| `EXPOSE` | Document the application's listening port. |
| `VOLUME` | Create a mount point for persistent data. |
| `ARG` | Define build-time variables. |
| `ENV` | Define environment variables. |
| `CMD` | Specify the default command. |
| `ENTRYPOINT` | Configure the executable. |
| `HEALTHCHECK` | Define a health check. |
| `SHELL` | Change the default shell. |
| `STOPSIGNAL` | Specify the container stop signal. |
| `ONBUILD` | Register deferred build instructions. |

---

# Build Context

The **build context** is the directory passed to the `docker build` command.

Example:

```bash
docker build .
```

Here, the current directory (`.`) becomes the build context.

Example structure:

```text
project/
│
├── Dockerfile
├── app.py
├── requirements.txt
├── assets/
└── README.md
```

All of these files are available to Docker during the build.

> [!IMPORTANT]
> `COPY` and `ADD` can only access files inside the build context.

For example, this works:

```dockerfile
COPY app.py /app/
```

This does **not**:

```dockerfile
COPY ../secret.txt /app/
```

because `secret.txt` is outside the build context.

---

# Comments

Comments begin with the `#` character.

Example:

```dockerfile
# Base image
FROM ubuntu

# Install Git
RUN apt update && apt install -y git
```

> [!NOTE]
> Comments are ignored during the build process.

---

# FROM

The `FROM` instruction specifies the **base image**.

Every Dockerfile (except special scratch images) starts with `FROM`.

## Syntax

```dockerfile
FROM <image>

FROM <image>:<tag>

FROM <image>@<digest>
```

Examples

```dockerfile
FROM ubuntu

FROM ubuntu:24.04

FROM nginx:latest
```

Using a specific version:

```dockerfile
FROM python:3.12
```

Using a digest:

```dockerfile
FROM ubuntu@sha256:<digest>
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `<image>` | Base image name. |
| `<tag>` | Specific image version. |
| `<digest>` | Immutable image digest. |

> [!IMPORTANT]
> Always prefer **specific image tags** over `latest` to ensure reproducible builds.

---

# RUN

The `RUN` instruction executes commands during the image build.

Each `RUN` instruction creates a **new image layer**.

## Syntax

```dockerfile
RUN <command>

RUN ["executable", "arg1", "arg2"]
```

Examples

```dockerfile
RUN apt update
```

Install packages:

```dockerfile
RUN apt update && apt install -y git curl
```

Exec form:

```dockerfile
RUN ["apt", "update"]
```

## Common Use Cases

- Install packages
- Download dependencies
- Compile software
- Create directories
- Configure the system

Example

```dockerfile
RUN mkdir /app
```

> [!TIP]
> Combine related commands into a single `RUN` instruction to reduce the number of image layers.

Good

```dockerfile
RUN apt update && \
    apt install -y git curl && \
    apt clean
```

Avoid

```dockerfile
RUN apt update

RUN apt install -y git

RUN apt install -y curl
```

because each instruction creates an additional image layer.

---

# COPY

The `COPY` instruction copies files and directories from the **build context** into the Docker image.

## Syntax

```dockerfile
COPY <source> <destination>

COPY [OPTIONS] <source> <destination>
```

---

## Parameters

| Parameter | Description |
|-----------|-------------|
| `<source>` | File or directory inside the build context. |
| `<destination>` | Destination path inside the image. |

---

## Common Options

| Option | Description |
|---------|-------------|
| `--chown=user:group` | Set file ownership. |
| `--chmod=<permissions>` | Set file permissions. |
| `--from=<stage>` | Copy files from another build stage. |

---

## Examples

Copy a single file

```dockerfile
COPY app.py /app/
```

Copy an entire directory

```dockerfile
COPY src/ /app/src/
```

Copy everything from the current directory

```dockerfile
COPY . .
```

Set ownership

```dockerfile
COPY --chown=app:app . /app
```

Copy from another build stage

```dockerfile
COPY --from=builder /app/build /usr/share/nginx/html
```

> [!IMPORTANT]
> `COPY` can only access files located inside the **build context**.

> [!TIP]
> Prefer `COPY` over `ADD` unless you specifically need one of `ADD`'s additional features.

---

# ADD

The `ADD` instruction copies files similarly to `COPY`, but also supports additional functionality.

## Syntax

```dockerfile
ADD <source> <destination>

ADD [OPTIONS] <source> <destination>
```

---

## Additional Features

- Automatically extracts local `.tar` archives.
- Can download files from remote URLs.
- Supports the same ownership and permission options as `COPY`.

---

## Examples

Copy a directory

```dockerfile
ADD assets/ /app/assets/
```

Extract a local archive

```dockerfile
ADD project.tar.gz /app/
```

Download a file

```dockerfile
ADD https://example.com/file.zip /downloads/
```

---

## COPY vs ADD

| COPY | ADD |
|------|-----|
| Copies files | Copies files |
| Recommended for most cases | Supports archive extraction |
| No URL support | Can download URLs |
| Simple and predictable | Additional behavior |

> [!IMPORTANT]
> Use `COPY` by default. Use `ADD` only when you specifically need archive extraction or remote URL downloads.

---

# WORKDIR

The `WORKDIR` instruction sets the working directory for all subsequent instructions.

## Syntax

```dockerfile
WORKDIR <directory>
```

---

## Example

```dockerfile
WORKDIR /app
```

Every following instruction executes relative to this directory.

```dockerfile
WORKDIR /app

COPY . .

RUN npm install

CMD ["npm", "start"]
```

---

## Multiple WORKDIR Instructions

```dockerfile
WORKDIR /app

WORKDIR src
```

Current directory becomes

```text
/app/src
```

---

> [!TIP]
> If the directory does not exist, Docker creates it automatically.

---

# LABEL

Labels store metadata inside an image.

## Syntax

```dockerfile
LABEL key=value
```

Multiple labels

```dockerfile
LABEL version="1.0" \
      maintainer="John Doe" \
      description="Example application"
```

---

## Common Labels

| Label | Description |
|--------|-------------|
| `version` | Application version |
| `maintainer` | Image maintainer |
| `description` | Short description |
| `license` | Software license |
| `vendor` | Organization or company |

---

Example

```dockerfile
LABEL version="2.1"

LABEL maintainer="john@example.com"
```

> [!NOTE]
> Labels do not affect container execution. They provide metadata only.

---

# USER

The `USER` instruction specifies which user executes subsequent instructions.

## Syntax

```dockerfile
USER <user>

USER <uid>
```

---

Examples

```dockerfile
USER root
```

```dockerfile
USER app
```

```dockerfile
USER 1000
```

---

Create and switch to a non-root user

```dockerfile
RUN useradd -m app

USER app
```

> [!IMPORTANT]
> Running containers as **non-root** improves security.

---

# EXPOSE

The `EXPOSE` instruction documents the port on which the application listens.

## Syntax

```dockerfile
EXPOSE <port>

EXPOSE <port>/<protocol>
```

---

Examples

```dockerfile
EXPOSE 80
```

```dockerfile
EXPOSE 443
```

```dockerfile
EXPOSE 8080/tcp
```

```dockerfile
EXPOSE 53/udp
```

---

> [!NOTE]
> `EXPOSE` **does not publish** a port to the host.

To publish a port:

```bash
docker run -p 8080:80 nginx
```

---

# VOLUME

The `VOLUME` instruction declares a mount point for persistent data.

## Syntax

```dockerfile
VOLUME <path>
```

or

```dockerfile
VOLUME ["<path>"]
```

---

Examples

```dockerfile
VOLUME /data
```

```dockerfile
VOLUME ["/var/lib/mysql"]
```

---

Typical use cases

- Databases
- Uploaded files
- Application data
- Logs

---

Example

```dockerfile
FROM mysql

VOLUME /var/lib/mysql
```

> [!IMPORTANT]
> Data stored in a volume remains available even after the container is removed.

---

## Typical Application Layout

A common Dockerfile structure looks like this:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "app.py"]
```

The instructions are executed in the following order:

```text
FROM
   │
WORKDIR
   │
COPY
   │
RUN
   │
COPY
   │
EXPOSE
   │
CMD
```

> [!TIP]
> Copy dependency files (such as `requirements.txt` or `package.json`) before copying the rest of the project. This allows Docker to reuse cached layers and significantly speeds up rebuilds.

---

# ARG

The `ARG` instruction defines variables that are available **only during the image build process**.

Build arguments are commonly used to customize image versions, package names, or build configurations.

## Syntax

```dockerfile
ARG <name>

ARG <name>=<default-value>
```

---

## Examples

Declare a build argument

```dockerfile
ARG VERSION
```

Provide a default value

```dockerfile
ARG VERSION=3.12
```

Use an argument

```dockerfile
ARG VERSION=3.12

FROM python:${VERSION}
```

Specify a value during build

```bash
docker build --build-arg VERSION=3.13 -t myapp .
```

---

## Properties

| Property | Description |
|----------|-------------|
| Scope | Build time only |
| Available during | `docker build` |
| Available inside running container | No |
| Can have a default value | Yes |
| Can be overridden | Yes (`--build-arg`) |

> [!IMPORTANT]
> `ARG` values are **not available** after the image has been built unless they are explicitly copied into an `ENV` variable.

---

# ENV

The `ENV` instruction defines environment variables that are stored inside the image.

Unlike `ARG`, environment variables are also available inside running containers.

## Syntax

```dockerfile
ENV <key>=<value>
```

or

```dockerfile
ENV <key> <value>
```

---

## Examples

```dockerfile
ENV APP_ENV=production
```

```dockerfile
ENV PORT=8080
```

Multiple variables

```dockerfile
ENV APP_ENV=production \
    PORT=8080 \
    DEBUG=false
```

Using an environment variable

```dockerfile
ENV APP_HOME=/app

WORKDIR $APP_HOME
```

---

## Properties

| Property | Description |
|----------|-------------|
| Scope | Build and runtime |
| Stored inside image | Yes |
| Available inside container | Yes |
| Can be overridden | Yes (`docker run -e`) |

Example

```bash
docker run -e PORT=5000 myapp
```

---

# ARG vs ENV

Although both define variables, they serve different purposes.

| Feature | ARG | ENV |
|----------|-----|-----|
| Build time | Yes | Yes |
| Runtime | No | Yes |
| Stored in image | No | Yes |
| Override during build | Yes | No |
| Override during run | No | Yes |

Workflow

```text
docker build
      │
     ARG
      │
Image created
      │
     ENV
      │
docker run
      ▼
Container
```

> [!TIP]
> Use `ARG` for build configuration and `ENV` for application configuration.

---

# CMD

The `CMD` instruction specifies the default command that is executed when a container starts.

A Dockerfile should contain **only one active `CMD` instruction**. If multiple `CMD` instructions exist, only the **last one** is used.

## Syntax

Shell form

```dockerfile
CMD command arguments
```

Exec form (recommended)

```dockerfile
CMD ["executable", "arg1", "arg2"]
```

---

## Examples

```dockerfile
CMD ["python", "app.py"]
```

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

Shell form

```dockerfile
CMD python app.py
```

---

## Properties

| Property | Description |
|----------|-------------|
| Executed when container starts | Yes |
| Can be overridden | Yes |
| Number allowed | One (last one wins) |

Override the default command

```bash
docker run ubuntu ls
```

Although the Dockerfile contains

```dockerfile
CMD ["bash"]
```

Docker executes

```text
ls
```

instead.

> [!IMPORTANT]
> Prefer the **exec form** (`["cmd","arg"]`) because it correctly handles signals and process management.

---

# ENTRYPOINT

`ENTRYPOINT` defines the executable that always runs when the container starts.

Unlike `CMD`, it is not easily replaced.

## Syntax

```dockerfile
ENTRYPOINT ["command"]
```

or

```dockerfile
ENTRYPOINT command
```

---

## Example

```dockerfile
ENTRYPOINT ["python"]
```

Run

```bash
docker run myapp app.py
```

Docker executes

```text
python app.py
```

---

## ENTRYPOINT with CMD

The two instructions are often used together.

```dockerfile
ENTRYPOINT ["python"]

CMD ["app.py"]
```

Result

```text
python app.py
```

Override only the arguments

```bash
docker run myapp test.py
```

Result

```text
python test.py
```

Workflow

```text
ENTRYPOINT
      │
      ▼
     CMD
      │
      ▼
Final command
```

---

# CMD vs ENTRYPOINT

| CMD | ENTRYPOINT |
|-----|------------|
| Default command | Main executable |
| Easily overridden | Normally preserved |
| Optional | Usually required for executable containers |
| Often provides arguments | Defines the executable |

> [!IMPORTANT]
> Use `ENTRYPOINT` when the container should always execute the same application. Use `CMD` to provide default arguments.

---

# HEALTHCHECK

The `HEALTHCHECK` instruction allows Docker to periodically verify whether a container is functioning correctly.

## Syntax

```dockerfile
HEALTHCHECK CMD <command>
```

Disable health checks

```dockerfile
HEALTHCHECK NONE
```

---

## Example

```dockerfile
HEALTHCHECK CMD curl --fail http://localhost:8080 || exit 1
```

---

## Common Options

| Option | Description |
|---------|-------------|
| `--interval` | Time between checks |
| `--timeout` | Maximum execution time |
| `--start-period` | Initial startup delay |
| `--retries` | Number of failures before unhealthy |

Example

```dockerfile
HEALTHCHECK \
--interval=30s \
--timeout=5s \
--retries=3 \
CMD curl --fail http://localhost || exit 1
```

---

## Health States

```text
Starting
     │
     ▼
 Healthy
     │
     ▼
Unhealthy
```

Check container health

```bash
docker ps
```

or

```bash
docker inspect <container>
```

> [!TIP]
> Health checks allow orchestration tools such as Docker Compose and Kubernetes to detect unhealthy containers automatically.

---

# Multi-stage Builds

Multi-stage builds allow you to use multiple `FROM` instructions within a single Dockerfile.

They are primarily used to:

- Reduce final image size.
- Separate build tools from the production environment.
- Improve security.
- Produce cleaner and more maintainable Dockerfiles.

---

## Build Workflow

```text
Build Stage
     │
     ▼
Compile Application
     │
     ▼
Copy Build Artifacts
     │
     ▼
Production Stage
     │
     ▼
Minimal Docker Image
```

---

## Syntax

```dockerfile
FROM <image> AS <stage-name>

...

FROM <image>

COPY --from=<stage-name> <source> <destination>
```

---

## Example

```dockerfile
FROM node:24 AS builder

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

RUN npm run build


FROM nginx:latest

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

---

## How It Works

1. The first stage builds the application.
2. Docker stores the generated artifacts.
3. The second stage starts from a clean image.
4. Only the required files are copied into the final image.

---

## Multiple Build Stages

```dockerfile
FROM node:24 AS dependencies

...

FROM node:24 AS builder

...

FROM nginx:latest AS production
```

Docker supports any number of build stages.

---

> [!IMPORTANT]
> Multi-stage builds significantly reduce image size by excluding development dependencies and build tools from the final image.

> [!TIP]
> Use multi-stage builds for production images whenever your application requires compilation or a build step.

---

# .dockerignore

The `.dockerignore` file specifies which files and directories should be excluded from the Docker build context.

---

## Why Use It?

Ignoring unnecessary files:

- Reduces build context size.
- Improves build performance.
- Prevents sensitive files from being copied.
- Produces cleaner images.

---

## Syntax

Each line contains one pattern.

```text
file.txt
directory/
*.log
```

---

## Example

```text
node_modules/
.git/
.vscode/
.env
README.md
*.log
```

---

## Project Structure

```text
project/
│
├── Dockerfile
├── .dockerignore
├── src/
├── node_modules/
├── .git/
└── .env
```

Files listed in `.dockerignore` are never sent to the Docker daemon during the build.

---

## Common Patterns

| Pattern | Description |
|--------|--------|
| `.git/` | Ignore Git metadata. |
| `node_modules/` | Ignore local dependencies. |
| `.env` | Ignore environment files. |
| `*.log` | Ignore log files. |
| `.DS_Store` | Ignore macOS metadata. |
| `.vscode/` | Ignore editor settings. |
| `target/` | Ignore Java build output. |
| `build/` | Ignore build artifacts. |

---

# Best Practices

Following Dockerfile best practices improves:

- Performance
- Security
- Readability
- Reproducibility
- Maintainability

---

## Use Official Images

Prefer official Docker images whenever possible.

Good:

```dockerfile
FROM python:3.12
```

Avoid:

```dockerfile
FROM latest
```

---

## Use Specific Image Versions

Good:

```dockerfile
FROM ubuntu:24.04
```

Avoid:

```dockerfile
FROM ubuntu:latest
```

Specific versions produce reproducible builds.

---

## Minimize Image Layers

Good:

```dockerfile
RUN apt update && \
    apt install -y curl git && \
    apt clean
```

Avoid:

```dockerfile
RUN apt update

RUN apt install -y curl

RUN apt install -y git
```

---

## Use Multi-stage Builds

Avoid shipping:

- Compilers
- Package managers
- Build tools
- Development dependencies

Use dedicated build and production stages.

---

## Prefer COPY over ADD

Good:

```dockerfile
COPY . .
```

Use `ADD` only when:

- Downloading remote files
- Extracting local archives

---

## Use Non-root Users

Good:

```dockerfile
RUN useradd -m app

USER app
```

Running containers as non-root users improves security.

---

## Keep Images Small

Smaller images provide:

- Faster downloads
- Faster deployments
- Reduced attack surface

Prefer:

- Official images
- Minimal base images
- Multi-stage builds

---

## Leverage Docker Cache

Good:

```dockerfile
COPY package*.json .

RUN npm install

COPY . .
```

Avoid:

```dockerfile
COPY . .

RUN npm install
```

Copying dependency files first significantly improves build performance.

---

## Add Health Checks

Good:

```dockerfile
HEALTHCHECK CMD curl --fail http://localhost:8080 || exit 1
```

Health checks improve reliability and help orchestration tools detect unhealthy containers.

---

## Keep Dockerfiles Readable

Use:

- Blank lines
- Comments
- Logical instruction order

Example:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "app.py"]
```

---

# Dockerfile Instruction Reference

| Instruction | Purpose | Build Time | Runtime |
|------------|------------|------------|------------|
| `FROM` | Specify the base image. | Yes | No |
| `RUN` | Execute build commands. | Yes | No |
| `COPY` | Copy files into the image. | Yes | No |
| `ADD` | Copy files with additional features. | Yes | No |
| `WORKDIR` | Set the working directory. | Yes | Yes |
| `LABEL` | Store image metadata. | Yes | Yes |
| `USER` | Specify the executing user. | Yes | Yes |
| `EXPOSE` | Document listening ports. | Yes | Yes |
| `VOLUME` | Define persistent storage. | Yes | Yes |
| `ARG` | Define build-time variables. | Yes | No |
| `ENV` | Define environment variables. | Yes | Yes |
| `CMD` | Specify the default command. | No | Yes |
| `ENTRYPOINT` | Specify the main executable. | No | Yes |
| `HEALTHCHECK` | Verify container health. | No | Yes |
| `SHELL` | Change the default shell. | Yes | No |
| `STOPSIGNAL` | Define the stop signal. | Yes | Yes |
| `ONBUILD` | Register deferred instructions. | Yes | No |

---
