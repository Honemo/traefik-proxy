# Just a simple Traefik Proxy

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)
- 🦄 Unicorns are not dead

## About <a name = "about"></a>

This is a template for your traefik proxies to manage your containers routers

## Getting Started <a name = "getting_started"></a>

To get start rename the `.env.example` file to `.env` and use it to customize your own router.

## Usage <a name = "usage"></a>

You can start your traefik router just starting the container using
`docker compose up -d`

## Add a another application to the router

To add another application to your new router add customs labels to your docker-compose files

Example :
```
services:
    yourserviceName:
        ...
        labels:
            ...
            - "traefik.enable=true"
            - "traefik.docker.network=web-applications"
            - "traefik.http.routers.webendpoint.entrypoints=web"
            - "traefik.http.routers.webendpoint.rule=Host(`yourhostame`)"
            - "traefik.http.routers.webendpoint.middlewares=webendpoint-middleware"
            - "traefik.http.routers.webendpoint-secure.tls=true"
            - "traefik.http.routers.webendpoint-secure.entrypoints=websecure"
            - "traefik.http.routers.webendpoint-secure.rule=Host(`yourhostame`)"
            - "traefik.http.middlewares.webendpoint-middleware.redirectscheme.scheme=https"
            - "traefik.http.middlewares.webendpoint-middleware.redirectscheme.permanent=true"
        networks:
            ...
            - web-applications
networks:
    ...
    web-applications:
        name: web-applications
        external: true
```
            
