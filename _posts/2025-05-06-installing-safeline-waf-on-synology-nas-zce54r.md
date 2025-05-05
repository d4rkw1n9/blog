---
title: Installing SafeLine WAF on Synology NAS
date: '2025-05-05 22:18:09'
permalink: /post/installing-safeline-waf-on-synology-nas-zce54r.html
tags:
  - synology
  - safeline
  - waf
  - security
  - nas
categories:
  - selfhosting
layout: single
published: true
---



# Installing SafeLine WAF on Synology NAS

In this post, I will explain the basic setup of the SafeLine WAF free edition on a Synology NAS.

# Prerequisites

I am assuming that you already have some general knowledge on how to install a docker stack on a Synology NAS, otherwise I can highly recommend to visit [mariushosting.com](), where Marius wrote some very helpful guides on how to use the container manager and also Portainer etc..

Furthermore, the automatic certificate creation in SafeLine WAF, requires port 80 to be free on the NAS. Make sure that the port is not used by any other application, otherwise certificate generation will fail with the error that port 80 is already in use.

# Installation

1. The first step is to create a folder in the location of your choice, like /volume1/docker/safeline.
2. Create a stack with the following compose:

```yaml
networks:
  safeline-ce:
    name: safeline-ce
    driver: bridge
    ipam:
      driver: default
      config:
        - gateway: ${SUBNET_PREFIX:?SUBNET_PREFIX required}.1
          subnet: ${SUBNET_PREFIX}.0/24
    driver_opts:
      com.docker.network.bridge.name: safeline-ce

services:
  postgres:
    container_name: safeline-pg
    restart: always
    image: ${IMAGE_PREFIX}/safeline-postgres${ARCH_SUFFIX}:15.2
    volumes:
      - ${SAFELINE_DIR}/resources/postgres/data:/var/lib/postgresql/data
      - /etc/localtime:/etc/localtime:ro
    environment:
      - POSTGRES_USER=safeline-ce
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD:?postgres password required}
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.2
    command: [postgres, -c, max_connections=600]
    healthcheck:
      test: pg_isready -U safeline-ce -d safeline-ce
  mgt:
    container_name: safeline-mgt
    restart: always
    image: ${IMAGE_PREFIX}/safeline-mgt${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG:?image tag required}
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - ${SAFELINE_DIR}/resources/mgt:/app/data
      - ${SAFELINE_DIR}/logs/nginx:/app/log/nginx:z
      - ${SAFELINE_DIR}/resources/sock:/app/sock
      - /var/run:/app/run
    ports:
      - ${MGT_PORT:-9443}:1443
    healthcheck:
      test: curl -k -f https://localhost:1443/api/open/health
    environment:
      - MGT_PG=postgres://safeline-ce:${POSTGRES_PASSWORD}@safeline-pg/safeline-ce?sslmode=disable
    depends_on:
      - postgres
      - fvm
    logging:
      driver: "json-file"
      options:
        max-size: "100m"
        max-file: "5"
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.4
  detect:
    container_name: safeline-detector
    restart: always
    image: ${IMAGE_PREFIX}/safeline-detector${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG}
    volumes:
      - ${SAFELINE_DIR}/resources/detector:/resources/detector
      - ${SAFELINE_DIR}/logs/detector:/logs/detector
      - /etc/localtime:/etc/localtime:ro
    environment:
      - LOG_DIR=/logs/detector
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.5
  tengine:
    container_name: safeline-tengine
    restart: always
    image: ${IMAGE_PREFIX}/safeline-tengine${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG}
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /etc/resolv.conf:/etc/resolv.conf:ro
      - ${SAFELINE_DIR}/resources/nginx:/etc/nginx
      - ${SAFELINE_DIR}/resources/detector:/resources/detector
      - ${SAFELINE_DIR}/resources/chaos:/resources/chaos
      - ${SAFELINE_DIR}/logs/nginx:/var/log/nginx:z
      - ${SAFELINE_DIR}/resources/cache:/usr/local/nginx/cache
      - ${SAFELINE_DIR}/resources/sock:/app/sock
    environment:
      - TCD_MGT_API=https://${SUBNET_PREFIX}.4:1443/api/open/publish/server
      - TCD_SNSERVER=${SUBNET_PREFIX}.5:8000
      - SNSERVER_ADDR=${SUBNET_PREFIX}.5:8000
      - CHAOS_ADDR=${SUBNET_PREFIX}.10
    ulimits:
      nofile: 131072
    network_mode: host       
  luigi:
    container_name: safeline-luigi
    restart: always
    image: ${IMAGE_PREFIX}/safeline-luigi${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG}
    environment:
      - MGT_IP=${SUBNET_PREFIX}.4
      - LUIGI_PG=postgres://safeline-ce:${POSTGRES_PASSWORD}@safeline-pg/safeline-ce?sslmode=disable
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - ${SAFELINE_DIR}/resources/luigi:/app/data
    logging:
      driver: "json-file"
      options:
        max-size: "100m"
        max-file: "5"
    depends_on:
      - detect
      - mgt
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.7
  fvm:
    container_name: safeline-fvm
    restart: always
    image: ${IMAGE_PREFIX}/safeline-fvm${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG}
    volumes:
      - /etc/localtime:/etc/localtime:ro
    logging:
      driver: "json-file"
      options:
        max-size: "100m"
        max-file: "5"
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.8
  chaos:
    container_name: safeline-chaos
    restart: always
    image: ${IMAGE_PREFIX}/safeline-chaos${REGION}${ARCH_SUFFIX}${RELEASE}:${IMAGE_TAG}
    logging:
      driver: "json-file"
      options:
        max-size: "100m"
        max-file: "10"
    environment:
      - DB_ADDR=postgres://safeline-ce:${POSTGRES_PASSWORD}@safeline-pg/safeline-ce?sslmode=disable
    volumes:
      - ${SAFELINE_DIR}/resources/sock:/app/sock
      - ${SAFELINE_DIR}/resources/chaos:/app/chaos
    networks:
      safeline-ce:
        ipv4_address: ${SUBNET_PREFIX}.10

```

3. add the following variables to your stack env variables:

```yaml
SAFELINE_DIR=/volume1/docker/safeline
IMAGE_TAG=latest
MGT_PORT=7443 #change it to your liking
POSTGRES_PASSWORD=SOMEPASSWORD #set the password for the postgres-database. 
SUBNET_PREFIX=172.22.222 #or whatever your choice is
IMAGE_PREFIX=chaitin
ARCH_SUFFIX=
RELEASE=
REGION=-g
```

4. Deploy and enjoy!
5. Continue to https://<your-nas-ip>:<chosen mgt_port> and set up

6. To get new login credentials, run this command on your NAS:

```shell
docker exec safeline-mgt resetadmin
```

Find more information on:

[https://docs.waf.chaitin.com/en/GetStarted/Deploy](https://docs.waf.chaitin.com/en/GetStarted/Deploy)

‍
