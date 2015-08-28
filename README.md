<!--
pandoc -o README.PDF README.md
-->

# Demo nginx in Docker

# Dockerfile
```
#
# Nginx Dockerfile
#
# https://github.com/dockerfile/nginx
#

# Pull base image.
FROM ubuntu:14.04

# Install Nginx.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install software-properties-common
RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.
#VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

COPY web /var/www/html
RUN chmod -R 755 /var/www/html

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
EXPOSE 443
```

# Commands

* Build the container
`docker build -t epflsti/nginx .`

* Launch the container
`docker run -p 8888:80 epflsti/nginx`

-d option to demonize

* Inspect the container
`docker exec -it epflsti/nginx /bin/bash`


# Links:
* [Docker nginx example](https://github.com/dockerfile/nginx)
* [Exampl with kitematic](https://docs.docker.com/kitematic/nginx-web-server/)
* [2048 source](https://github.com/gabrielecirulli/2048/archive/master.zip)
