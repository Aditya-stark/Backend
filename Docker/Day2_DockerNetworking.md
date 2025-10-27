
## Day 2 — Docker networking (step by step)

### Overview

- External ports on the host are closed by default for security.
- If you want a container to accept connections from outside the host, you must expose or map ports explicitly.
- Containers talk to each other over an internal virtual network; that traffic stays on the host.
- By default each container connects to the bridge network (a private virtual network).
- The bridge network routes outgoing traffic through the host using NAT (Network Address Translation).
- Containers on the same bridge network can reach each other without mapping ports with `-p`.

---

### Simple rules (best practices)

1. Give each application its own custom network to isolate services.
2. Use Docker's defaults when you want simplicity; customize networks when you need isolation, routing, or multi-host features.
3. You can attach a container to multiple networks or to none (if you want it isolated).
4. Use host network mode (`--net=host`) only when you need the container to use the host network stack directly.
5. Choose the network driver based on needs: `bridge` (default), `host`, `overlay` (swarm/inter-host), `macvlan`, etc.

---

### Common commands (examples)

1) Run a container and map a host port to a container port

```
docker run -p 80:80 --name webhost -d nginx
```

This starts an Nginx container named `webhost` and maps port 80 on the host to port 80 inside the container.

2) Check which host ports a container uses

```
docker container port webhost
```

3) Get the container's internal IP address

```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' webhost
```

### Quick recap

- The default bridge network allows internal container-to-container communication.
- You must explicitly expose or map ports for external access to containers.
- Creating custom networks improves security and control.
- Docker networking is flexible: use defaults for quick start and custom networks for production setups.