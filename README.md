# INSTALAR DOCKER
## Ubuntu
````bash=
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
````
## Amazon Linux
````bash=
sudo yum install docker
sudo service docker start
sudo systemctl enable docker
sudo service docker status
sudo usermod -aG docker $USER
````


## Docker Compose
````bash=
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
````

En caso de que no tengas curl instalado, puedes instalarlo usando el siguiente comando:
````bash=
yum install curl
````
Luego tienes que asignar permisos de ejecución al Docker Compose binario:
````
sudo chmod +x /usr/local/bin/docker-compose
````

Y ahora, para garantizar que no haya problemas al usar la herramienta en el terminal, tendrás que hacer un enlace simbólico al sistema:
````
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
````

Finalmente, verifica la versión instalada:
````
sudo docker-compose --version
````

### instalar docker compose de UNA
````
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo docker-compose --version
````

### seccion deploy de docker swarm en manager
````
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
````

### seccion deploy de docker swarm en worker
````
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
      placement:
        constraints:
          - node.role == worker
          - node.hostname == ip-172-31-80-9
      update_config:
        delay: 1m
        parallelism: 1
        failure_action: rollback
````

### volumen en docker swarm
````
    volumes:
      - type: bind
        source: /home/ubuntu/apps/feanware/data
        target: /var/lib/postgresql/data
````
