docker 安装 命令
```sh
docker pull library/mysql:5.7.44
```


docker run

```sh
docker run --name mysql5.7 \
           -e MYSQL_ROOT_PASSWORD=root \
           -v /docker/volume/mysql5.7:/var/lib/mysql \
           -p 3306:3306 \
           -d mysql:5.7.44
```

```sh
docker run --name mysql57 \  容器名
           -e MYSQL_ROOT_PASSWORD=your_password \ root密码
           -v /path/on/host/mysql/data:/var/lib/mysql \ 磁盘映射
           -p 3306:3306 \ 端口映射
           -d mysql:5.7
```


