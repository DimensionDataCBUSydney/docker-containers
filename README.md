## Docker containers for Dimension Data R&D research projects

This repository contains containers for Docker for applications that are under research

# Using Docker on Dimension Data Cloud

1. Deploy the Ubuntu 14.04 base image in the MCP
2. Login to the server, run "wget -qO- https://get.docker.com/ | sh" to install docker-engine
3. Install the git client "apt-get install git"
4. Clone this repository "git clone http://github.com/DimensionDataCBUSydney/docker-containers"
5. Choose the application "cd docker-containers/{app}"
6. Build the container
7. Run the container