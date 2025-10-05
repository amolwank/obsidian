Docker System and Info:
```
docker version  -> Show docker client and server vesions.
docker info -> Display detailed system-wide information
docker system df ->show disk usage by docker
docker system prune -a -> clean unused images, containers, networks.
```
Images
```
docker images          -> List all images
docker pull <image>    -> Download image from the Docker Hub.
docker rmi <image-id>  -> Remove an image
docker build -t <image-name>:<tag> . -> Build image from Dockerfile
docker tag <image> <repo>:<tag> -> Tag image for repository
docker push <repo>:<tag> -> Push image to Docker Hub.

```
Containers:
```
docker ps --> List Running containers.
docker ps -a -> List all containers (including stopped)
docker run -it <image> /bin/bash -> Run a container with interactive shell.
docker run -d --name <name> <image> -> Run container in detached mode.
docker stop <container-id> -> Stop the running container.
docker start <container-id> -> Start a stopped container.
docker restart <container-id> -> Restart container.
docker rm <container-id> -> Remove the container.
docker exce -it <container-id> /bin/bash -> Get inside container shell

```
Logs and Debugging:
```
docker logs <container-id> ->View container logs.
docker logs -f <container-id> -> Follow logs in real-time
docker inspect <container-id> -> Detailed contanier info (JSON)
docker top <container-id> -> Show running processing inside the container.
docker stats -> show resurces usage of running containers.

```
Volumes and Networks:
```
docker volume ls -> List volumes.
docker volumn rm <volume> -> Remove Volume
docker network ls -> List networks.
docker network inspect <network> -> Inspect network details.
docker network create <network> --> Create Network.
```

Docker Compose
```
docker-compose up -d --> Start services in background.
docker-compose down --> Stop and remove containers.
docker-compose ps --> Show running containers from compose.
docker-compose logs -f --> Follow logs.
docker-compose build --> Build services defined in docker-compose.yaml
```

Shortcut Tips:
```
docker container prune --> Remove all stopped containers.
docker image prune -a  --> Remove all unused images.
docker volume prune    --> Remove all unused volumes
```
