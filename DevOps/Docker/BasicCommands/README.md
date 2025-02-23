# 🚀 Important Docker Commands and Descriptions

## 🛠 Basic Docker Commands

| Command            | Description                                   |
| ------------------ | --------------------------------------------- |
| `docker --version` | Check the installed Docker version.           |
| `docker info`      | Display system-wide information about Docker. |
| `docker help`      | Show help for Docker commands.                |

## 📦 Container Management

| Command                                    | Description                                             |
| ------------------------------------------ | ------------------------------------------------------- |
| `docker run <image>`                       | Create and start a container from an image.             |
| `docker run -d <image>`                    | Run a container in detached mode (background).          |
| `docker run -it <image> /bin/bash`         | Run a container interactively with a shell.             |
| `docker ps`                                | List running containers.                                |
| `docker ps -a`                             | List all containers (including stopped ones).           |
| `docker stop <container_id>`               | Stop a running container.                               |
| `docker start <container_id>`              | Start a stopped container.                              |
| `docker restart <container_id>`            | Restart a running/stopped container.                    |
| `docker rm <container_id>`                 | Remove a stopped container.                             |
| `docker logs <container_id>`               | View logs of a container.                               |
| `docker exec -it <container_id> /bin/bash` | Access a running container’s shell.                     |
| `docker inspect <container_id>`            | Get detailed information about a container.             |
| `docker stats`                             | Display real-time resource usage of running containers. |

## 🖼 Image Management

| Command                                   | Description                             |
| ----------------------------------------- | --------------------------------------- |
| `docker images`                           | List all available Docker images.       |
| `docker pull <image>`                     | Download an image from Docker Hub.      |
| `docker push <image>`                     | Upload an image to Docker Hub.          |
| `docker build -t <image_name> .`          | Build a Docker image from a Dockerfile. |
| `docker rmi <image_id>`                   | Remove an image from the system.        |
| `docker tag <image_id> <repo_name>:<tag>` | Tag an image with a name and version.   |
| `docker history <image>`                  | Show the history of an image.           |

## 📂 Volumes and Data Persistence

| Command                                     | Description                    |
| ------------------------------------------- | ------------------------------ |
| `docker volume create <volume_name>`        | Create a new Docker volume.    |
| `docker volume ls`                          | List all Docker volumes.       |
| `docker volume inspect <volume_name>`       | Get details about a volume.    |
| `docker volume rm <volume_name>`            | Remove a volume.               |
| `docker run -v <volume_name>:/data <image>` | Mount a volume to a container. |

## 🌍 Networking

| Command                                           | Description                            |
| ------------------------------------------------- | -------------------------------------- |
| `docker network ls`                               | List all Docker networks.              |
| `docker network create <network_name>`            | Create a custom network.               |
| `docker network inspect <network_name>`           | Get details about a network.           |
| `docker network connect <network> <container>`    | Connect a container to a network.      |
| `docker network disconnect <network> <container>` | Disconnect a container from a network. |

## 🔄 Docker Compose

| Command                | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| `docker-compose up`    | Start containers using `docker-compose.yml`.              |
| `docker-compose up -d` | Start containers in detached mode.                        |
| `docker-compose down`  | Stop and remove all containers from `docker-compose.yml`. |
| `docker-compose ps`    | List containers managed by `docker-compose`.              |

## 🔧 Docker System Cleanup

| Command                  | Description                                     |
| ------------------------ | ----------------------------------------------- |
| `docker system df`       | Show Docker disk usage.                         |
| `docker system prune`    | Remove unused images, containers, and networks. |
| `docker image prune`     | Remove unused images.                           |
| `docker container prune` | Remove stopped containers.                      |
| `docker volume prune`    | Remove unused volumes.                          |


