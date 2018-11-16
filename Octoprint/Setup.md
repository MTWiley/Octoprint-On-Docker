# mjpg-streamer - https://store.docker.com/community/images/mrwyss/mjpg-streamer
docker run -d -p 8080:80 --device=/dev/video0 --name=mjpg-streamer mrwyss/mjpg-streamer

# octoprint - https://store.docker.com/community/images/mrwyss/octoprint
docker run -d --link mjpg-streamer -p 5000:5000 --device=/dev/ttyUSB0 --name=octoprint_linked mrwyss/octoprint

#haproxy - https://hub.docker.com/r/nmarus/haproxy-certbot/
mkdir /docker/haproxy/config
mkdir /docker/haproxy/letsencrypt
mkdir /docker/haproxy/certs.d
