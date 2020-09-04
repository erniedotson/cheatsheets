# Docker Cheat sheet

## Table of Contents

<!-- markdownlint-disable MD004 -->

<!-- toc -->

- [Containers](#containers)
- [Images](#images)
- [Volumes](#volumes)
- [Cleaning up](#cleaning-up)
- [Docker-compose](#docker-compose)
- [Info](#info)
- [References](#references)

<!-- tocstop -->

<!-- markdownlint-enable MD004 -->

## Containers

| Action | Command |
| ------ | ------- |
| List running containers | `docker container ls` |
| List all containers | `docker container ls -a` |
| Run and attach to container | `docker run -it --rm alpine sh` |
| Execute a command in container | `docker exec $CONTAINER echo "Hello from container!"` |
| Stop a running container through SIGTERM | `docker container stop $CONTAINER` |
| Stop a running container through SIGKILL | `docker container kill $CONTAINER` |
| Stop all running containers | `docker stop $(docker ps -aq)` |
| Remove one or more containers | `docker container rm $CONTAINER` |
| Remove Exited Containers | `docker rm $(docker ps -q -f "status=exited")` |
| Delete all running and stopped containers | `docker container rm -f $(docker ps -aq)` |
| Create Alpine Heredoc container | `docker build -t htop - << EOF`<br/>`FROM alpine`<br/>`RUN apk --no-cache add htop`<br/>`EOF` |

## Images

| Action | Command |
| ------ | ------- |
| List images | `docker image ls` |
| List all (intermediate) images | `docker image ls -a` |
| Delete image | `docker image rm alpine:3.4` |
| Remove Dangling Images | `docker rmi $(docker images -q -f "dangling=true")` |
| Build an image from Dockerfile | `docker build -t myimage:1.0 .` |
| Pull image | `docker pull myimage:1.0` |
| (Re)Tag an image | `docker tag myimage:1.0 myrepo/myimage:2.0` |
| Push image | `docker push myrepo/myimage:2.0` |

## Volumes

| Action | Command |
| ------ | ------- |
| Remove Dangling Volumes | `docker volume rm $(docker volume ls -q -f "dangling=true")` |

## Cleaning up

| Action | Command |
| ------ | ------- |
| Report disk space usage | `docker system df` |
| Remove unused containers, networks, images, (optionally volumes) | `docker system prune [-a] [--volumes] [-f]` |
| Remove all unused local volumes | `docker volume prune [-f]` |
| Remove all unused networks | `docker network prune [-f]` |
| Remove all stopped containers | `docker container prune [-f]` |
| Remove unused images | `docker image prune [-a] [-f]` |

## Docker-compose

| Action | Command |
| ------ | ------- |
| View docker-compose file AFTER .env substitution | `docker-compose config` |
| Start (create or resume) containers | `docker-compose up -d` |
| List containers | `docker-compose ps` |
| Stop containers | `docker-compose stop` |
| Stop and remove containers | `docker-compose down` |
| Tail container logs | `docker-compose logs -f` |

## Info

| Action | Command |
| ------ | ------- |
| Get basic version information | `docker --version` |
| Get Detailed version information | `docker version` |
| Display system-wide information | `docker info` |

## References

- [Docker Reference Documentation](https://docs.docker.com/reference)
