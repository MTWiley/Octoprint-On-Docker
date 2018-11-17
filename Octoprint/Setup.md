##################################################################################################################

## Install Docker

- https://docs.docker.com/install/

##################################################################################################################

## mjpg-streamer

- https://store.docker.com/community/images/mrwyss/mjpg-streamer
- https://github.com/MrWyss/mjpg-streamer-docker

### Start the mjpg-streamer container

    docker run -d \
      --restart=always \
      -p 8081:80 \
      --device=/dev/video0 \
      --name=mjpg-streamer \
      mrwyss/mjpg-streamer

##################################################################################################################

## Octoprint

- https://store.docker.com/community/images/mrwyss/octoprint
- https://github.com/MrWyss/octoprint-docker

### Create the persistent directories on the docker machine

    mkdir /docker/octoprint/github
    mkdir /docker/octoprint/data

### Copy in the haproxy.cfg file

    cd $ThisRepoLocation/Octoprint/
    cp haproxy.cfg /docker/haproxy/config/

### Start the octoprint container

    docker run -d \
      --restart=always \
      --p 5000:5000 \
      --device=/dev/ttyUSB0 \ #
      -v /docker/octoprint/github/:/octoprint \
      -v /docker/octoprint/data/:/data \
      --name=octoprint \
      mrwyss/octoprint

##################################################################################################################

## HAProxy

- https://hub.docker.com/r/nmarus/haproxy-certbot/
- https://github.com/nmarus/docker-haproxy-certbot

### Create the directories on the docker machine

    mkdir /docker/haproxy/config
    mkdir /docker/haproxy/letsencrypt
    mkdir /docker/haproxy/certs.d

### Copy in the haproxy.cfg file

    cd $ThisRepoLocation/Octoprint/
    cp HAProxy/haproxy.cfg /docker/haproxy/config/

### Start the haproxy container

    docker run -d \
      --restart=always \
      --name haproxy-certbot \
      --cap-add=NET_ADMIN
      -p 80:80 \
      -p 443:443 \
      -v /docker/haproxy/config:/config \
      -v /docker/haproxy/letsencrypt:/etc/letsencrypt \
      -v /docker/haproxy/certs.d:/usr/local/etc/haproxy/certs.d \
      nmarus/haproxy-certbot

### Get Initial Certificate

    docker exec haproxy-certbot certbot-certonly \
      --domain wiley-apex.ddns.net \
      --email michaeltwiley@gmail.com

### Pickup Changes to Certs

    docker exec haproxy-certbot haproxy-refresh

### Renew Certificate

    docker exec haproxy-certbot certbot-renew
