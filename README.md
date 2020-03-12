#!/bin/bash
#Description: clean my docker images
#Date: 3/9/2020
#Author: Ruben Louis jean

echo -e "\n Cleanup docker images"
# Do not run if removal already in progress.
pgrep "docker rm" && exit 0

# Remove Dead and Exited containers.
docker rm $(docker ps -a | grep "Dead\|Exited" | awk '{print $1}'); true

# It will fail to remove images currently in use.
docker rmi $(docker images -qf dangling=true); true

# Clean up unused docker volumes
docker volume rm $(docker volume ls -qf dangling=true); true

