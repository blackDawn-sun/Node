#docker-compose #docker
1.下载docker compose
官网：[GitHub - docker/compose: Define and run multi-container applications with Docker · GitHub](https://github.com/docker/compose)
下载对应版本的docker compose
这里选择的是 v2.36.2 版本，
tag地址：[Release v2.36.2 · docker/compose · GitHub](https://github.com/docker/compose/releases/tag/v2.36.2)
下载地址： [Fetching Title#268n](https://github.com/docker/compose/releases/download/v2.36.2/docker-compose-linux-x86_64)
2.将下载后的文件 改名为 docker-compose 并传入Linux服务器  /usr/local/bin 文件夹下

3.增加可执行权限
```sh
sudo chmod +x /usr/local/bin/docker-compose
```
4.测试安装
```sh
docker-compose --version
```


### bridge 网络使用
```yml
version: '3.9'

services:
  postgres:
    image: postgres:16
    container_name: pgsql
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
    ports:
      - "5432:5432"
    volumes:
      - /docker/docker-volume/pgsql16:/var/lib/postgresql/data
    networks:
      - dev-bridge

networks:
  dev-bridge:
    driver: bridge

```