## Correr contenedor
```yml
version: '3.3'
services:
  mqtt:
    container_name: mosquitto
    image: eclipse-mosquitto: 1.6
    ports:
      - "1883:1883"
      - "9001:9001"
    volumes:
      - /docker/mosquitto/config:/mqtt/config
      - /docker/mosquitto/log: /mqtt/log
      - /docker/mosquitto/data/:/mqtt/data
```

## Crear contraseña
```
cd /mosquitto/config
mosquitto_passwd -c passwd [user]
```

## modificar el mosquitto.conf
```
password_file /mosquitto/config/passwd
```

## reiniciar docker container
```
sudo docker restart mosquitto
```
