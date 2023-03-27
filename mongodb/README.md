# Docker compose mongodb

````yml
version: '3.1'


services:


  mongo:
    image: mongo
    restart: always
    container_name: monog_db
    ports:
      - 8080:27017
    environment:
      MONGO_INITDB_DATABASE: db
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    volumes:
      - ./mongo-volume:/data/db


  mongo-express:
    image: mongo-express
    restart: always
    container_name: mongo_manager
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: example
      ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/



# docker exec -it mongodb bash
# mongo -u “user” -p “password”

````