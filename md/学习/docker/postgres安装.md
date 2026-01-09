#docker #postgres 
## 管理工具
[SQLynx 数据库管理工具](../../软件/SQLynx%20数据库管理工具.md)(免费)

## docker 安装 命令
```sh
docker pull postgres:15
```


## docker run

```sh
docker run -d \
  --name postgres \
  -p 3406:5432 \
  -e POSTGRES_PASSWORD=root\
  -v /my/local/data:/var/lib/postgresql/data \
  postgres:latest
```

```sh
docker run -d \
  --name postgres \ 容器名
  -p 5432:5432 \ 端口映射
  -e POSTGRES_PASSWORD=yourpassword \ 密码
  -v /my/local/data:/var/lib/postgresql/data \ 空间映射
  postgres:latest
```

容器查看


主从复制
