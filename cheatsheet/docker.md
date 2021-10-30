# docker

## [Dockerhub Images](https://hub.docker.com)

## Basic Commands

```bash
# check if docker
cat /proc/1/cgroup

# see all imaages
docker images

# see all containers
docker ps --all

# remove
docker rm <CONTAINER_ID>
docker rmi <IMAGE_ID>

# run
sudo docker run -it <IMAGE_ID> bash

# remove all containers
docker rm $(docker ps -a -f status=exited -q) 

# remove all images
docker rmi $(docker images -a -q)
```
