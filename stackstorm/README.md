# st2docker

## Requirements

To play around with this docker image, docker must be installed on your system.

## Steps

* Git clone this repo to your boxL

```bash
git clone https://github.com/DimensionDataCBUSydney/docker-containers.git
```

* Change in to docker directory:

```bash
cd docker-containers/stackstorm
```

* Build st2 docker image:

```bash
docker build -t st2 .
```

* Run a container with the image:

```bash
docker run -it st2
```

* Change the password for testu inside container:

```bash
htpasswd /etc/st2/htpasswd testu
```

* Update the configuration of the Dimension Data pack with your cloud control credentials

```bash
vi /opt/stackstorm/packs/st2_dimensiondata/config.yaml
```

* Login to the UI

http://{ip}:8080/


For more information please refer to the documentation -
http://docs.stackstorm.com/
