# Nginx-Virtual-Host-Docker-Container


Followed Links - 

https://dolphinandmermaids.com/blog/docker-nginx-letsencrypt/  *
https://www.bogotobogo.com/DevOps/Docker/Docker-Compose-Nginx-Reverse-Proxy-Multiple-Containers.php
https://gist.github.com/morgangiraud/9c49d596991dbb47be6b52bfa3bce862





Task - Nginx virtual hosting inside docker container - with SSL 


Create DockerFile for Nginx -

FROM nginx:alpine
COPY nginx.conf /etc/nginx/nginx.conf


After that we create a docker-compose file -

Let’s start by creating our main Docker Compose file, that will launch our nginx proxy and Let’s Encrypt companion containers. In a separate folder called proxy create file docker-compose.yml with contents below:


version: '3'   # Version of the Docker Compose file format
services:

  webserver:
    build: .
    container_name: webserver
    restart: on-failure
    tty: true
    ports:
      - "80:80"
      - "81:81"
      - "443:443"
    volumes:
      - ./sites/:/usr/share/nginx/html
      - ./demoone/:/usr/share/nginx/html/demoone
      - ./ssl/:/etc/ssl
      
      
-------------------------------

Command -

docker-compose build

docker-compose up -d


Docker Compose will look for a file named docker-compose.yml in the current folder and launch all services (containers) that are described in there. In this case it will launch nginx proxy and Let’s Encrypt companion containers. Also, because we trying to launch it for the first time it will build images first.
Flag -d means that we want to run our containers in the background (detached mode).

----------------------------------------------------------------------------------------------------------

Use the following command to check containers status:



docker ps
