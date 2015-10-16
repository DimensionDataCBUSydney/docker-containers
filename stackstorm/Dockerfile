# Pull base image.
FROM ubuntu:14.04

# Disable prompts
ENV DEBIAN_FRONTEND noninteractive

# Reset policy-rc.d
RUN echo "#!/bin/sh\nexit 101" > /usr/sbin/policy-rc.d
RUN chmod +x /usr/sbin/policy-rc.d

# Add the PostgreSQL PGP key to verify their Debian packages.
# It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# Add PostgreSQL's repository. It contains the most recent stable release
#     of PostgreSQL, ``9.3``.
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

# Install ``python-software-properties``, ``software-properties-common`` and PostgreSQL 9.3
#  There are some warnings (in red) that show up during the build. You can hide
#  them by prefixing each apt-get statement with DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y python-software-properties software-properties-common postgresql-9.3 postgresql-client-9.3 postgresql-contrib-9.3

RUN    /etc/init.d/postgresql start

# Install Python
RUN \
  apt-get update && \
    apt-get install -y curl python python-dev python-pip python-virtualenv openssh-server && \
      apt-get install -y python-prettytable python-yaml git && \
        rm -rf /var/lib/apt/lists/*

# Set environment variable to Docker
ENV CONTAINER DOCKER

RUN cd /root && curl -sS -k -O https://ops.stackstorm.net/releases/st2/scripts/st2_deploy.sh

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