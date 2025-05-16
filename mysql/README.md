```yml
version: '3.3'
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: 'db'
      # So you don't have to use root, but you can if you like
      MYSQL_USER: 'user'
      # You can use whatever password you like
      MYSQL_PASSWORD: 'password'
      # Password for root access
      MYSQL_ROOT_PASSWORD: 'password'
    ports:
      # <Port exposed> : <MySQL Port running inside container>
      - '3306:3306'
    expose:
      # Opens port 3306 on the container
      - '3306'
      # Where our data will be persisted
    volumes:
      - my-db:/var/lib/mysql
# Names our volume
volumes:
  my-db:
```

---

```yml
version: '3.8'

services:
  db:
    image: mysql:8.0
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - "3306:3306"
    volumes:
      - type: bind
        source: ./data
        target: /var/lib/mysql
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
```


---

```yml
version: '3.8'
services:
  db:
    image: mysql:8.0
    restart: always
    environment:
      - MYSQL_DATABASE=quotes
      - MYSQL_ROOT_PASSWORD=mauFJcuf5dhRMQrjj
    ports:
      - '3306:3306'
    volumes:
      - db:/var/lib/mysql
```

## Recuperar un backUp en Docker
- docker exec my_msql /usr/bin/mysql -u root --password=test_pass -e 'CREATE DATABASE testdb;'
- docker exec -i my_mysql /usr/bin/mysql -u root --password=test_pass testdb < dump_on_host.sql
- docker exec -it my_mysql /usr/bin/mysql -u root --password=test_pass testdb mysql> SHOW TABLES;
