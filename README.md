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