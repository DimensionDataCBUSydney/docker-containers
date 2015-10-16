# Docker containers for Dimension Data R&D research projects

This repository contains containers for Docker for applications that are under research

## Using Docker on Dimension Data Cloud

1. Deploy the Ubuntu 14.04 base image in the MCP
2. Login to the server, run "wget -qO- https://get.docker.com/ | sh" to install docker-engine

Now you have 2 choices, use from docker hub or use from source

## Using these containers from Docker Hub

3. Go to https://hub.docker.com/u/dimensiondataresearch/dashboard/ and choose an image
4. Pull the image using the instructions on the repository page

## Building these containers from source

3. Install the git client "apt-get install git"
4. Clone this repository 
```git clone http://github.com/DimensionDataCBUSydney/docker-containers"```
5. Choose the application 
```cd docker-containers/{app}```
6. Build the container
```docker build -t test_container .```
7. Run a container with the image:
```docker run -it test_container```
