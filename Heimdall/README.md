# Docker compose Heimdall

````yml
version: "2.1"
services:
  heimdall:
    image: lscr.io/linuxserver/heimdall
    container_name: heimdall
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Bogota
    volumes:
      - ./appdata/config:/config
    ports:
      - 82:80
    restart: unless-stopped
````
