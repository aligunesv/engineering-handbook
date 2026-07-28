# Docker Images

A Docker image is a read-only template used to create containers. It contains the application, runtime, libraries, dependencies, and configuration needed to run software consistently across different environments.

---

## Listing Images

List all locally available images:

```bash
docker image ls
```

or

```bash
docker images
```

---

## Pulling an Image

Download an image from a registry:

```bash
docker pull nginx
```

Download a specific version:

```bash
docker pull nginx:1.27
```

---

## Searching for Images

Search Docker Hub for images:

```bash
docker search nginx
```

---

## Building an Image

Build an image from a Dockerfile in the current directory:

```bash
docker build -t myapp:latest .
```

Specify a different Dockerfile:

```bash
docker build -f Dockerfile.dev -t myapp:dev .
```

---

## Tagging an Image

Create another tag for an existing image:

```bash
docker tag myapp:latest myrepo/myapp:v1
```

List image tags:

```bash
docker image ls
```

---

## Inspecting an Image

View detailed information about an image:

```bash
docker image inspect nginx
```

---

## Viewing Image History

Display the layers used to build an image:

```bash
docker history nginx
```

---

## Removing Images

Remove an image:

```bash
docker image rm nginx
```

Remove multiple images:

```bash
docker image rm nginx alpine ubuntu
```

Force removal:

```bash
docker image rm -f nginx
```

---

## Removing Unused Images

Delete dangling images:

```bash
docker image prune
```

Delete all unused images:

```bash
docker image prune -a
```

---

## Saving an Image

Export an image to a tar archive:

```bash
docker save -o nginx.tar nginx
```

---

## Loading an Image

Import an image from a tar archive:

```bash
docker load -i nginx.tar
```

---

## Pushing an Image

Upload an image to a registry:

```bash
docker push myrepo/myapp:v1
```

---

## Image Naming Convention

```text
registry/repository:tag
```

Examples:

```text
nginx
nginx:latest
ubuntu:24.04
docker.io/library/nginx:latest
ghcr.io/example/myapp:v1.0
```

---

## Image Layers

Docker images are composed of multiple read-only layers.

Example:

```text
Ubuntu Base Image
        │
        ▼
Python Runtime
        │
        ▼
Application Dependencies
        │
        ▼
Application Code
```

Each instruction in a Dockerfile typically creates a new layer.

---

## Image vs Container

| Image | Container |
|--------|-----------|
| Read-only template | Running instance of an image |
| Immutable | Writable |
| Used to create containers | Executes the application |
| Can exist without running | Exists only while created |

---

## Common Commands

| Command | Purpose |
|---------|---------|
| `docker image ls` | List local images |
| `docker pull` | Download an image |
| `docker build` | Build an image |
| `docker tag` | Create a new tag |
| `docker push` | Upload an image |
| `docker image inspect` | Show image details |
| `docker history` | Show image layers |
| `docker image rm` | Remove an image |
| `docker image prune` | Remove unused images |
| `docker save` | Export an image |
| `docker load` | Import an image |

---

## Cheat Sheet

```text
docker image ls
docker pull <image>
docker search <image>
docker build -t <name>:<tag> .
docker tag <image> <new-image>
docker push <image>
docker image inspect <image>
docker history <image>
docker image rm <image>
docker image prune -a
docker save -o image.tar <image>
docker load -i image.tar
```
