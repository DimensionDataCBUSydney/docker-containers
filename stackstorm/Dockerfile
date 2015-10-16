# Pull base image.
FROM ubuntu:14.04

# Disable prompts
ENV DEBIAN_FRONTEND noninteractive

# Reset policy-rc.d
RUN echo "#!/bin/sh\nexit 101" > /usr/sbin/policy-rc.d
RUN chmod +x /usr/sbin/policy-rc.d

# Install Python
RUN \
  apt-get update && \
    apt-get install -y curl python python-dev python-pip python-virtualenv openssh-server && \
      apt-get install -y python-prettytable python-yaml git && \
        rm -rf /var/lib/apt/lists/*

# Set environment variable to Docker
ENV CONTAINER DOCKER

RUN cd /root && curl -sS -k -O https://raw.githubusercontent.com/tonybaloney/st2/master/tools/st2_deploy.sh

RUN bash -c 'chmod +x /root/st2_deploy.sh'

RUN bash -c '/root/st2_deploy.sh latest || exit 2'

ADD . /root/st2/

RUN bash -c 'chmod +x /root/st2/start.sh'

RUN bash -c '/root/st2/start.sh'

RUN bash -c 'st2 run packs.install packs=chef,puppet,octopusdeploy,salt,ansible repo_url=https://github.com/StackStorm/st2contrib.git'

RUN bash -c 'st2 run packs.install packs=st2_dimensiondata repo_url=https://github.com/DimensionDataCBUSydney/st2_dimensiondata.git'

# auth service
EXPOSE 9100
# api server
EXPOSE 9101
# webui
EXPOSE 8080