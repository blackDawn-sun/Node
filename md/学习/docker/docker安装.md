#docker
## 1. 安装依赖 
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
## 2. 安装对应镜像源(华为)
```shell
wget -O /etc/yum.repos.d/docker-ce.repo https://mirrors.huaweicloud.com/docker-ce/linux/centos/docker-ce.repo
```
## 3. 修改镜像源地址
```shell
sudo sed -i 's/download.docker.com/mirrors.huaweicloud.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo 
```
## 4. 更新索引文件并安装
```shell
sudo yum makecache fast  
sudo yum install docker-ce //安装docker
```
补充命令:
```shell
yum list docker-ce.x86_64 --showduplicates | sort -r //从高到低列出Docker-ce的版本
yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io //指定版本（docker-ce-18.09.9）进行安装
yum install docker-ce-18.09.9 docker-ce-cli-18.09.9 containerd.io
```
## 5. 启动docker

```sh
systemctl start docker

systemctl enable docker   //开机自启

docker run hello-world    /Helloword 测试安装成功
```
## 6. 配置docker国内镜像源

> tbtnsge26dvc5a.xuanyuan.run  轩辕专属域名(失效)
> 

```
cd /etc/docker/
vim /etc/docker/daemon.json
```
```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://hub.rat.dev",
    "https://docker-0.unsee.tech"
  ]
}
```
## 7. 重启docker服务
```sh
sudo systemctl daemon-reload
sudo systemctl restart docker

```

## 8. 给用户增加docker用户组
```sh
sudo groupadd docker
sudo usermod -aG docker bg // bg是当前用户
newgrp docker //切换用户组, 重启shell
```

## 9.docker 网络桥接

### 创建桥接网络
方法1：使用默认配置
```sh
docker network create test-network
```
方法2：指定子网和网关（推荐）
```sh
docker network create \
  --driver bridge \
  --subnet=172.20.0.0/16 \
  --gateway=172.20.0.254 \
  test-network
```
参数详解：

参数	说明	示例值
--driver bridge	指定网络驱动为桥接模式	bridge
--subnet	子网地址范围	172.20.0.0/16
--gateway	网关地址	172.20.0.254
--ip-range	容器可分配IP范围	172.20.1.0/24
--aux-address	保留IP地址	
### 查询网络信息
```sh
docker network ls #查所有网络信息
docker network inspect test-network #查详细信息
```
示例返回
```sh
[root@aos01 ~]# docker network inspect test-network
[
    {
        "Name": "test-network",
        "Id": "0df765dce9792404bb7866681adcde1f90a62981132d9b8a59b6827b139eed62",
        "Created": "2026-05-11T17:12:29.104069175+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]

```
### 删除网络
```sh
 docker network rm test-network
```

docker compose 
# [docker compose](docker%20compose.md)