# Docker commands — quick cheat sheet

This file lists common Docker commands, grouped by topic. Each command includes a short explanation. Use these as quick reminders.

## Images

- List all local images

```
docker images
```

- Delete an image (by name:tag or image ID)

```
docker rmi <image_name>:<tag>
docker rmi <image_id>
```

- Remove dangling / unused images

```
docker image prune
```

- Build an image from a Dockerfile (tag the image)

```
docker build -t <image_name>:<version> .
```

- Build without using cache

```
docker build --no-cache -t <image_name>:<version> .
```

## Containers

- List all containers (running and stopped)

```
docker ps -a
```

- List only running containers

```
docker ps
```

- Create and run a new container (foreground)

```
docker run <image_name>
```

If the image isn't local, Docker pulls it from Docker Hub first.

- Run a container in the background (detached)

```
docker run -d --name <container_name> <image_name>
```

- Run a container with a custom name

```
docker run --name <container_name> <image_name>
```

- Map a host port to a container port (host:container)

```
docker run -p <host_port>:<container_port> --name <container_name> <image_name>
```

- Set environment variables inside a container

```
docker run -e ENV_VAR=value --name <container_name> <image_name>
```

- Start or stop an existing container

```
docker start <container_name_or_id>
docker stop <container_name_or_id>
```

- Inspect a container (shows detailed JSON)

```
docker inspect <container_name_or_id>
```

- Remove a container (must be stopped first)

```
docker rm <container_name_or_id>
```

## Troubleshooting

- Fetch logs of a container

```
docker logs <container_name_or_id>
```

- Open an interactive shell inside a running container

```
docker exec -it <container_name_or_id> /bin/bash
# or if bash not available
docker exec -it <container_name_or_id> sh
```

## Docker Hub (push / pull / search)

- Pull an image from Docker Hub

```
docker pull <image_name>:<tag>
```

- Push an image to Docker Hub (image must be tagged with your username/repo)

```
docker push <username>/<image_name>:<tag>
```

- Login to Docker Hub

```
docker login
# or
docker login -u <username>
```

- Logout from Docker Hub

```
docker logout
```

- Search for images on Docker Hub

```
docker search <image_name>
```

## Volumes

- List all volumes

```
docker volume ls
```

- Create a named volume

```
docker volume create <volume_name>
```

- Remove a named volume

```
docker volume rm <volume_name>
```

- Mount a named volume in a container

```
docker run -v <volume_name>:<container_path> --name <container_name> <image_name>
# or using --mount
docker run --mount type=volume,src=<volume_name>,dst=<container_path> --name <container_name> <image_name>
```

- Mount an anonymous volume (Docker creates the volume)

```
docker run -v <container_path> --name <container_name> <image_name>
```

- Create a bind mount (host directory mapped into container)

```
docker run -v <host_path>:<container_path> --name <container_name> <image_name>
# or using --mount
docker run --mount type=bind,src=<host_path>,dst=<container_path> --name <container_name> <image_name>
```

- Remove unused local volumes

```
docker volume prune
```

## Network

- List networks

```
docker network ls
```

- Create a network

```
docker network create <network_name>
```

- Remove a network

```
docker network rm <network_name>
```

- Remove unused networks

```
docker network prune
```

---

Tip: Use `--help` with any Docker command to see full options (for example `docker run --help`).
