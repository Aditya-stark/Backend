# Docker Cheat Sheet (Day 1)

A concise, sequential reference for basic Docker commands and common systemd/service operations. Corrected, formatted and organized for quick reading.

## Table of contents

- Quick reference
- Images: pull / list / remove
- Containers: run / list / stop / remove
- Inspect / execute / logs
- Managing Docker as a systemd service
- Shell & environment tips
- Next steps

## Quick reference

- Check Docker version:

```bash
docker --version
```

- Check Docker running containers:

```bash
docker ps            # running containers
docker ps -a         # all containers (including stopped)
```

## Images

- Pull an image from Docker Hub (or another registry):

```bash
sudo docker pull <image-name>[:tag]
```

- List local images:

```bash
docker images
```

- Remove a local image (use image ID or name:tag):

```bash
docker rmi <image-id-or-name:tag>
```

Note: `docker rm` is for removing containers; `docker rmi` removes images.

## Containers

- Run a container (detached):

```bash
docker run -d --name my-container <image-name>
```

- Run interactively (with a TTY):

```bash
docker run -it --rm <image-name> /bin/bash
```

- Stop and remove a container:

```bash
docker stop <container-id-or-name>
docker rm <container-id-or-name>
```

## Inspecting and interacting

- Execute a command inside a running container:

```bash
docker exec -it <container-id-or-name> <command>
# example: docker exec -it my-container bash
```

- View container logs:

```bash
docker logs -f <container-id-or-name>
```

- Show detailed information about a container or image:

```bash
docker inspect <container-or-image>
```

## Managing Docker service (systemd)

Use `systemctl` to control the Docker daemon on systemd-based systems:

```bash
sudo systemctl status docker     # check status
sudo systemctl start docker      # start daemon
sudo systemctl stop docker       # stop daemon
sudo systemctl restart docker    # restart daemon
sudo systemctl enable docker     # start on boot
sudo systemctl disable docker    # disable start on boot
```

If you installed Docker without systemd privileges, use `sudo` where needed.

## Shell & environment tips

- Reload your shell configuration (e.g., after adding PATH changes):

```bash
source ~/.bashrc
```

- If you want to run docker commands without `sudo`, add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
# then log out and back in (or run: newgrp docker)
```

## Example workflow (sequence)

1. Check Docker daemon is running:

```bash
sudo systemctl status docker
```

2. Pull an image:

```bash
sudo docker pull ubuntu:24.04
```

3. Run the image interactively:

```bash
docker run -it --name demo-ubuntu ubuntu:24.04 bash
```

4. In another terminal, list containers and view logs:

```bash
docker ps -a
docker logs demo-ubuntu
```

5. Stop and remove the container when done:

```bash
docker stop demo-ubuntu
docker rm demo-ubuntu
```

## Next steps

- Add notes on Docker Compose for multi-container apps.
- Add examples for building images with `Dockerfile` (docker build).
- Explain networking, volumes and data persistence.

---

If you'd like, I can also add a short section with `docker build` and a sample `Dockerfile`, or convert this into a printable cheat-sheet. Which would you prefer?





  