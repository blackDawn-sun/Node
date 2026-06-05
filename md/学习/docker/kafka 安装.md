先安装[zookeeper 安装](zookeeper%20安装.md) 
docker-compose

```yml
version: '3.9'

networks:
  dev-bridge:
    driver: bridge

services:
  kafka:
    image: wurstmeister/kafka:3.9.1
    container_name: kafka_server
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka_server:9092
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /docker/docker-volume/kafka:/var/run/docker.sock
    networks:
      - dev-bridge

```