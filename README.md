# nginx-simple-reverse-proxy

Simple nginx dockerized reverse proxy that pulls the proxied address from the environment.

Example usage:

`docker run -e DESTINATION=http://localhost:1337 ghcr.io/joamla96/nginx-simple-reverse-proxy:latest`

or in a stack, behind a traefik reverse proxy (proxy-ception?):

```
version: "3.3"
services:
  eco-:
    image: ghcr.io/joamla96/nginx-simple-reverse-proxy:latest
    restart: always
    networks:
      - public
    environment:
      - DESTINATION=http://10.20.40.14:3001
    deploy:
      labels:
        - "traefik.enable=true"
        - "traefik.http.services.ecoe.loadbalancer.server.port=80"
        - "traefik.http.routers.eco.rule=Host(`eco.domain.tld`)"
        - "traefik.http.routers.eco.entrypoints=websecure"
        - "traefik.http.routers.eco.tls.certresolver=letsencryptresolver"

networks:
  public:
    external: true
```
