# ----------------------------------
# Pterodactyl Core Dockerfile
# Environment: Java
# Minimum Panel Version: 0.6.0
# ----------------------------------
FROM openjdk:17-jdk-alpine

MAINTAINER fexa1819 gunit1895@gmail.com

RUN apk add --no-cache --update curl ca-certificates openssl git tar bash sqlite fontconfig \
    && adduser --disabled-password --home /home/container container

USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

COPY ./install.sh /install.sh

CMD ["/bin/bash","chmod +x /install.sh","/install.sh"]