# Day 2 Application Development

Normally you'd need to install Node, MySQL, and other programs on your computer. With Docker, you just need Docker Desktop. Everything else runs in containers, and you can share this exact setup with your whole team.

## Steps 
- Clone and start a development project
- Make changes to the backend and frontend
- See the changes immediately

## Start the project

1. First download or clone any project 

2. Once we have the project start the development environment using Docker Compose in the project folder.

```
    $ docker compass watch 
```

After that you will see an output that shows container images being pulled down container starting and more. 

## What happen when you run this command 
1. Docker reads the Compose file (`docker-compose.yml`) to determine which services and settings to run.
2. Docker downloads images — if needed, it pulls pre-built images (for example, Node, MySQL) from a registry.
3. Docker starts containers — it creates and runs the defined containers (frontend, backend, database, etc.).
4. Docker networks services — it connects the containers so they can communicate according to the Compose configuration.
5. Live watch/rebuild — if your setup uses bind mounts or a file watcher, code changes are detected and the running containers are updated automatically.
6. App is ready — open your browser at `http://localhost` (or the configured port) to use the application.


