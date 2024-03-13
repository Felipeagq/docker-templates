Email:    admin@example.com
Password: changeme


````yml
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
````

---
```
version: '3'

services:

  app:
    image: 'jc21/nginx-proxy-manager:latest'
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - type: bind
        source: ./data
        target: /data
      - type: bind
        source: ./letsencrypt
        target: /etc/letsencrypt
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
      placement:
        constraints:
          - node.role == manager
      update_config:
        order: start-first
        delay: 1m
        parallelism: 1
        failure_action: rollback
```
