docker compose 
```yml
version: '3.9'

networks:
  dev-bridge:
    driver: bridge

services:
  zookeeper:
    image: wurstmeister/zookeeper:3.6.4
    container_name: zookeeper
    ports:
      - "2181:2181"
    networks:
      - dev-bridge
```