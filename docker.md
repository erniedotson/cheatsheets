# Docker Cheat sheet

## Table of Contents

<!-- markdownlint-disable MD004 -->

<!-- toc -->

- [Kill Containers](#kill-containers)
- [Cleaning up](#cleaning-up)

<!-- tocstop -->

<!-- markdownlint-enable MD004 -->

## Kill Containers

| Action | Command |
| ------ | ------- |
| List running containers | `docker container ls` or `docker ps` |
| List all containers | `docker container ls -a` or `docker ps -a` |
| Kill one or more running containers | `docker kill $ID`

## Cleaning up

| Action | Command |
| ------ | ------- |
| Report disk space usage | `docker system df` |
| Remove unused containers, networks, images, (optionally volumes) | `docker system prune [-a] [--volumes] [-f]` |
| Remove all unused local volumes | `docker volume prune [-f]` |
| Remove all unused networks | `docker network prune [-f]` |
| Remove all stopped containers | `docker container prune [-f]` |
| Remove unused images | `docker image prune [-a] [-f]` |
