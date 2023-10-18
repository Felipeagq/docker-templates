````yml
version: '3.8'
services:
  db:
    image: postgres:14.1-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_DB=database_name
      - POSTGRES_PASSWORD=postgres
    ports:
      - '5432:5432'
    volumes:
      - data:/var/lib/postgresql/data

````
----
# Docker Swarm
````yaml
version: '3.8'
services:
  db:
    image: postgres:14.1-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_DB=database_name
      - POSTGRES_PASSWORD=postgres
    ports:
      - '5432:5432'
    volumes:
      - type: bind
        source: /home/ubuntu/apps/feanware/data
        target: /var/lib/postgresql/data
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
      placement:
        constraints:
          - node.role == worker
          - node.hostname == ip-172-31-80-32
      update_config:
        delay: 1m
        parallelism: 1
        failure_action: rollback
````
