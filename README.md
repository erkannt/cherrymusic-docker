# Simple docker image for [CherryMusic](http://www.fomori.org/cherrymusic/)

## Usage

    docker build -t holizz/cherrymusic .
    docker run -ti --rm \
               -v /path/to/music:/music \
               -v /path/to/persistent/data:/root/.local \
               -p 3000:3000 \
               --name cherrymusic holizz/cherrymusic

Then visit: http://localhost:3000/

Replace /path/to/music with the path to your music directory.

If you want to change the port you have to change it in the Dockerfile too.

## Compose

    version: '3'
   
    services:
      cherrymusic:
        image: holizz/cherrymusic
        networks:
          - traefik_public
        volumes:
          - /path/to/music:/music
          - /path/to/persistent/data:/root/.local

When building the docker image yourself replace `image: holizz/cherrymusic` with `build: ./cherrymusic-docker`.

When using [traefik](https://docs.traefik.io/configuration/backends/docker/) you can use the following:

       labels:
        - traefik.frontend.rule=Host:cherry.yourdomain.net
        - traefik.port=3000
