# Docker Commands Reference

## Docker Container Commands

| Command | Description |
|--------|-------------|
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (including stopped ones) |
| `docker run -it ubuntu bash` | Start a container in interactive mode |
| `docker stop <container_id>` | Stop a running container |
| `docker rm <container_id>` | Remove a container |
| `docker logs <container_id>` | Show logs of a container |

## Docker Image Commands

| Command | Description |
|--------|-------------|
| `docker images` | List local images |
| `docker build -t myimage .` | Build an image from Dockerfile |
| `docker rmi <image_id>` | Remove a Docker image |
| `docker pull ubuntu` | Download Ubuntu image |
| `docker tag <image_id> newname` | Tag an image with a new name |
