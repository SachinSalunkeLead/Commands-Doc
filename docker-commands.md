# 🐳 Docker Commands Reference

A quick reference for commonly used Docker CLI commands, grouped by category.

---

## 📦 Container Commands

| Command | Description |
|--------|-------------|
| `docker run -it ubuntu bash` | Run Ubuntu container in interactive terminal |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running + stopped) |
| `docker stop <container_id>` | Stop a running container |
| `docker start <container_id>` | Start a stopped container |
| `docker restart <container_id>` | Restart a container |
| `docker rm <container_id>` | Remove a container |
| `docker logs <container_id>` | View logs of a container |
| `docker exec -it <container_id> bash` | Run command in running container |

---

## 🖼️ Image Commands

| Command | Description |
|--------|-------------|
| `docker images` | List local images |
| `docker pull <image_name>` | Download image from Docker Hub |
| `docker build -t myimage .` | Build image from Dockerfile |
| `docker rmi <image_id>` | Remove an image |
| `docker tag <image_id> newname` | Tag image with new name |

---

## 💾 Volume Commands

| Command | Description |
|--------|-------------|
| `docker volume create myvolume` | Create a volume |
| `docker volume ls` | List volumes |
| `docker volume inspect myvolume` | Inspect a volume |
| `docker volume rm myvolume` | Remove a volume |

---

## 🌐 Network Commands

| Command | Description |
|--------|-------------|
| `docker network ls` | List networks |
| `docker network create mynet` | Create a custom network |
| `docker network inspect mynet` | Inspect network details |
| `docker network rm mynet` | Remove a network |
| `docker run --network=mynet ...` | Run container on specific network |

---

## 🧩 Docker Compose

| Command | Description |
|--------|-------------|
| `docker-compose up` | Start services defined in `docker-compose.yml` |
| `docker-compose up -d` | Start services in detached mode |
| `docker-compose down` | Stop and remove containers/networks/volumes |
| `docker-compose ps` | List containers managed by Compose |
| `docker-compose logs` | View logs from Compose services |
| `docker-compose build` | Build services |
| `docker-compose exec <service> bash` | Open shell inside a service container |

---

## 🧹 Cleanup Commands

| Command | Description |
|--------|-------------|
| `docker system prune` | Remove all stopped containers, networks, images not used |
| `docker container prune` | Remove all stopped containers |
| `docker volume prune` | Remove all unused volumes |
| `docker image prune` | Remove dangling images |

---

✍️ **Tip**: Replace `<container_id>` or `<image_id>` with the actual ID or name.

---

📌 **Keep this updated** as you discover more Docker features!
