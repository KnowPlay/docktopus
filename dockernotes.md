# Docker Notes

## About

Docker is an open-source platform that automates the deployment of applications inside lightweight, portable containers.

## Features

- **Consistency**: operates the same in various environments
- **Isolation**: each runs independently, reducing conflicts
- **Portability**: "build once, run anywhere" across different environments
- **Efficiency**: containers share the host system’s kernel and are not burdened with overhead

## Components

### Images

> Templates used to create containers
- e.g. `docker pull <name>` to download the specific image
  
### Containers

> Instances created from Docker images that house the applications
- e.g. `docker run -it <name> /bin/bash` to run the specific container interactively
  
### Docker Daemon

> Runs on the host machine and listens for Docker API requests to manage Docker objects such as images, containers, networks, and volumes.
- e.g. When you want to start a new container with `docker run -d -p 80:80 nginx`, Daemon:
  - Receives the command
  - Fetches the necessary image(if it's not already locally available)
  - Creates the container
  - Manages its lifecycle

### Docker Client

> Allows interactions with the Docker Daemon
  - Primary user interface to Docker 
  - Issue commands to the Docker Daemon
- e.g. `docker ps` lists all currently running containers
  
### Docker Hub

> [Container Image Repository](https://hub.docker.com/) allows users to push and pull container images.

> [Official Images](https://hub.docker.com/search?type=image&image_type=official) provides a vast collection of container images sourced from commercial software vendors, open-source projects, and independent developers. These official images are vetted by Docker for security and performance.

> [Automated Builds](https://docs.docker.com/docker-hub/builds/) can automatically build container images from source code in an external repository (like GitHub or Bitbucket) and push them to Docker Hub whenever the source code is updated.

> [Webhooks](https://docs.docker.com/docker-hub/webhooks/) allows triggering actions in other services or toolchains when a new image is pushed to a repository on Docker Hub. This feature is useful for integrating Docker Hub with continuous integration workflows.

## Processes

### Create Docker Images

#### Dockerfile: most used keywords

> FROM `image[:tag] [AS name]`
```
# choose the base image to use for the new image
FROM ubuntu:20.04
```
> WORKDIR
```
# set the working directory for the full instructions
WORKDIR /app
```
> COPY `[--chown=<user>:<group>] <src>... <dest>`
```
# copy the files and directories from the build content to the image
COPY . /app
```
> RUN `command`
```
# execute command in shell during image build
RUN npm run dev
```
> EXPOSE `<port> [<port>/<protocol>...]`
```
# inform docker that the container will listen on specific ports
EXPOSE 3000
```
> ENV `KEY=VALUE`
```
# sets environmental variables during build
ENV NODE_ENV=production
```
> ARG `<name>[=<default value>]`
```
# defines build time variables
ARG NODE_VERSION=20
```
> VOLUME `["/data]`
```
# create mount point for external storage
VOLUME /myvol
```
> {CMD != ENTRYPOINT}: CMD is a default executable, flexible, and can be overridden, while ENTRYPOINT is a fixed starting point and can't be easily overridden. If both CMD and ENTRYPOINT is used, it's passed through ENTRYPOINT.
> CMD `["executable", "param1", "param2"]`
```
# default command to execute when the container starts
CMD ["param1", "param2"]
```
> ENTRYPOINT `CMD ["executable", "param1", "param2"]`
```
# specifies the default exeutable to be run when the container starts 
CMD command "param1 param2
```