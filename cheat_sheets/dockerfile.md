# This is basic Dockerfile and some useful stuff
```
# Simple nginx image, index.html needs to be in the same file as Dockerfile is
FROM ubuntu:bionic

ENV NGINX_VERSION 1.14.0-0ubuntu1.7

RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION

WORKDIR /var/www/html/

ADD index.html ./

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

STOPSIGNAL SIGTERM
HEALTHCHECK CMD curl localhost:80
```
### Build and test
```
docker build -t <tag> .
docker run --name <tag> -d -p 8080:80 custom-nginx
curl localhost:8080
```