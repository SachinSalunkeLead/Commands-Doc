# 🐳 Docker Commands Reference

A quick reference for commonly used Docker CLI commands, grouped by category.

---

## 📦 Container Commands

| Command | Description |
|--------|-------------|
| `docker run -it ubuntu bash` | Run Ubuntu container in interactive terminal |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running + stopped) |
| `docker start <container_id>` | Start a stopped container |
| `docker stop <container_id>` | Stop a running container |
| `docker restart <container_id>` | Restart a container |
| `docker rm <container_id>` | Remove a container |
| `docker logs <container_id>` | View logs of a container |
| `docker exec -it <container_id> bash` | Run command inside a running container |
| `docker inspect <container_id>` | Inspect container details |
| `docker top <container_id>` | Display running processes inside container |
| `docker stats` | Show real-time resource usage of containers |
| `docker attach <container_id>` | Attach your terminal to a running container |
| `docker pause <container_id>` | Pause all processes in a container |
| `docker unpause <container_id>` | Resume a paused container |
| `docker kill <container_id>` | Forcefully stop a container |
| `docker rename <old_name> <new_name>` | Rename a container |
| `docker cp <container_id>:/file /host/path` | Copy file from container to host |
| `docker cp /host/path <container_id>:/file` | Copy file from host to container |

---

## ⚙️ Multiple Container Operations

| Command | Description |
|--------|-------------|
| `docker stop $(docker ps -q)` | Stop all running containers |
| `docker rm $(docker ps -a -q)` | Remove all containers (stopped + running) |
| `docker start $(docker ps -a -q)` | Start all containers |
| `docker restart $(docker ps -q)` | Restart all running containers |
| `docker logs -f $(docker ps -q)` | Follow logs of all running containers (not ideal for many) |
| `docker inspect $(docker ps -q)` | Inspect all running containers |
| `docker top $(docker ps -q)` | Show processes in all running containers (one by one) |

---

✍️ **Tip:** Use `$(docker ps -q)` to select all container IDs in shell commands.

## 🔘 Selected Multiple Containers

| Command | Description |
|--------|-------------|
| `docker stop container1 container2` | Stop selected containers by name or ID |
| `docker rm container1 container2` | Remove selected containers |
| `docker start container1 container2` | Start selected containers |
| `docker restart container1 container2` | Restart selected containers |
| `docker logs container1 container2` | View logs of selected containers (sequentially) |
| `docker inspect container1 container2` | Inspect multiple containers |
| `docker top container1 container2` | View running processes inside selected containers |

---

## 🔍 Tips for Selecting Specific Containers

You can use `docker ps` + `grep` or `awk` to select by name, image, label, etc.:

```bash
# Example: Stop containers with name starting with "web"
docker stop $(docker ps -q --filter "name=web")

# Remove containers created from 'nginx' image
docker rm $(docker ps -a -q --filter ancestor=nginx)

# Restart containers with label "env=dev"
docker restart $(docker ps -q --filter "label=env=dev")


---

## 🖼️ Image Commands

| Command | Description |
|--------|-------------|
| `docker images` | List all local Docker images |
| `docker pull <image>` | Download an image from Docker Hub |
| `docker build -t myimage .` | Build image from Dockerfile in current dir |
| `docker tag <image_id> username/repo:tag` | Tag an image with a new name |
| `docker push username/repo:tag` | Push image to Docker Hub |
| `docker rmi <image_id>` | Remove an image |
| `docker inspect <image_id>` | Inspect metadata of an image |
| `docker save -o image.tar <image>` | Save image as `.tar` archive file |
| `docker load -i image.tar` | Load image from `.tar` archive file |
| `docker history <image>` | View image layer history |
| `docker image prune` | Remove unused/dangling images |
| `docker image ls` | Alias for `docker images` |
| `docker image rm <image>` | Remove image (same as `docker rmi`) |

---

## 🧯 Remove All Images

| Command | Description |
|--------|-------------|
| `docker rmi $(docker images -q)` | Remove **all** Docker images |
| `docker image prune -a` | Remove all unused images (not just dangling ones) |

---

## 🔘 Selected Multiple Images

| Command | Description |
|--------|-------------|
| `docker rmi image1 image2` | Remove selected images by name or ID |
| `docker tag image1 newname1 && docker tag image2 newname2` | Tag multiple images manually |
| `docker push image1 image2` | Push selected images (tagged) to registry |

---

## 🔍 Filtered Image Operations

| Command | Description |
|--------|-------------|
| `docker images --filter "dangling=true"` | List dangling (unused) images |
| `docker rmi $(docker images -q --filter "dangling=true")` | Remove all dangling images |
| `docker images --filter "reference=nginx"` | List images matching a specific name |
| `docker images | grep '<pattern>'` | Filter images by pattern (name, tag, etc.) |

---

## 📦 Export/Import Images (Backup/Move)

| Command | Description |
|--------|-------------|
| `docker save -o myimage.tar myimage:latest` | Save image as a `.tar` archive |
| `docker load -i myimage.tar` | Load image from a saved archive |

---

## 💾 Volume Commands

| Command | Description |
|--------|-------------|
| `docker volume create myvolume` | Create a named volume |
| `docker volume ls` | List all Docker volumes |
| `docker volume inspect myvolume` | Show detailed info about a volume |
| `docker volume rm myvolume` | Remove a specific volume |
| `docker volume prune` | Remove all unused volumes |

---

## ⚙️ All Volumes Operations

| Command | Description |
|--------|-------------|
| `docker volume ls -q` | List only volume names (quiet mode) |
| `docker volume rm $(docker volume ls -q)` | Remove **all volumes** (use with caution) |
| `docker volume inspect $(docker volume ls -q)` | Inspect all volumes one by one |
| `docker volume prune` | Remove all **dangling (unused)** volumes |

---

## 🔘 Selected Multiple Volumes

| Command | Description |
|--------|-------------|
| `docker volume rm vol1 vol2` | Remove selected volumes |
| `docker volume inspect vol1 vol2` | Inspect multiple specific volumes |
| `docker volume ls | grep myvol` | List volumes matching a pattern |
| `docker volume rm $(docker volume ls -q | grep myvol)` | Remove volumes by name pattern |

---

## 🔍 Volume Usage with Containers

| Command | Description |
|--------|-------------|
| `docker run -v myvolume:/data ubuntu` | Mount a named volume to a container |
| `docker run -v /host/path:/container/path ubuntu` | Mount a host directory as a volume |
| `docker inspect <container_id>` | Check volume mounts used by a container |
| `docker container prune` | Delete stopped containers (releases volume usage) |

---

## 📦 Backup/Restore Volumes (manually)

| Command | Description |
|--------|-------------|
| `docker run --rm -v myvolume:/volume -v $(pwd):/backup ubuntu tar czf /backup/vol.tar.gz -C /volume .` | Backup a volume to host |
| `docker run --rm -v myvolume:/volume -v $(pwd):/backup ubuntu tar xzf /backup/vol.tar.gz -C /volume` | Restore a volume from host archive |

---

## 🌐 Network Commands

| Command | Description |
|--------|-------------|
| `docker network ls` | List all Docker networks |
| `docker network inspect <network_name>` | Show detailed info about a network |
| `docker network create <network_name>` | Create a custom bridge network |
| `docker network rm <network_name>` | Remove a specific Docker network |

---

## ⚙️ Custom Network Creation

| Command | Description |
|--------|-------------|
| `docker network create --driver bridge mynet` | Create a custom bridge network |
| `docker network create --driver overlay myoverlay` | Create an overlay network (Swarm) |
| `docker network create --subnet=192.168.10.0/24 mycustomnet` | Create a network with a custom subnet |

---

## 🔗 Connect/Disconnect Containers to Networks

| Command | Description |
|--------|-------------|
| `docker network connect mynet mycontainer` | Connect container to a specific network |
| `docker network disconnect mynet mycontainer` | Disconnect container from a network |
| `docker run --network=mynet ...` | Start a container connected to a specific network |

---

## 🧯 Remove Multiple Networks

| Command | Description |
|--------|-------------|
| `docker network rm net1 net2` | Remove multiple specific networks |
| `docker network rm $(docker network ls -q)` | Remove **all** networks (except default ones – fails silently if in use) |
| `docker network prune` | Remove all **unused** networks |

---

## 🔍 Filtered Network Operations

| Command | Description |
|--------|-------------|
| `docker network ls --filter driver=bridge` | List only bridge networks |
| `docker network ls --filter name=mynet` | List networks with name matching "mynet" |
| `docker network inspect $(docker network ls -q --filter driver=bridge)` | Inspect all bridge networks |

---

## 📋 Default Docker Networks

Docker creates the following default networks automatically:

| Network | Driver | Purpose |
|--------|--------|---------|
| `bridge` | bridge | Default for containers on a single host |
| `host` | host | Removes network isolation; container shares host stack |
| `none` | null | Disable networking entirely |
| `overlay` | overlay | Multi-host networking (used with Docker Swarm) |


---

# 🧩 Docker Compose Commands

A cheat sheet for working with `docker-compose`, used to define and manage multi-container Docker applications.

---

## 🚀 Basic Commands

| Command | Description |
|--------|-------------|
| `docker-compose up` | Start all services defined in `docker-compose.yml` |
| `docker-compose up -d` | Start services in detached mode (runs in background) |
| `docker-compose down` | Stop and remove all services, networks, and volumes |
| `docker-compose start` | Start existing services without recreating |
| `docker-compose stop` | Stop running services |
| `docker-compose restart` | Restart services |
| `docker-compose build` | Build images specified in the compose file |
| `docker-compose pull` | Pull service images from Docker registry |
| `docker-compose push` | Push built images to registry (if tagged) |

---

## 🛠️ Service Management

| Command | Description |
|--------|-------------|
| `docker-compose exec <service> bash` | Run a bash shell inside a running service container |
| `docker-compose run <service> <command>` | Run one-off command in a new container |
| `docker-compose logs` | Show logs from all services |
| `docker-compose logs -f` | Follow logs in real-time |
| `docker-compose ps` | List running services/containers |
| `docker-compose config` | Validate and view the final configuration |
| `docker-compose rm` | Remove stopped service containers |

---

## 📁 Using Different Compose Files

| Command | Description |
|--------|-------------|
| `docker-compose -f docker-compose.prod.yml up` | Use a different Compose file |
| `docker-compose -f docker-compose.dev.yml -f override.yml up` | Combine multiple Compose files (second overrides first) |
| `docker-compose -f <file> config` | Validate specific Compose file |
| `COMPOSE_FILE=docker-compose.dev.yml docker-compose up` | Set Compose file via environment variable |

---

## 🧹 Cleanup

| Command | Description |
|--------|-------------|
| `docker-compose down --volumes` | Remove volumes created by Compose |
| `docker-compose down --rmi all` | Remove containers, networks, and all images |
| `docker-compose down --remove-orphans` | Remove containers not defined in Compose file |

---

## 🧪 Tips & Best Practices

| Tip | Description |
|-----|-------------|
| Use `.env` file | Compose automatically loads variables from `.env` file in same directory |
| Named volumes | Recommended to avoid data loss across `up`/`down` cycles |
| Use `depends_on` | Ensure services start in order (not a wait-for-ready mechanism) |
| Combine Compose with `.dockerignore` | Optimize builds by ignoring unnecessary files |


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
