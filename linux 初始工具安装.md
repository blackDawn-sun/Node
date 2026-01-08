
> [!NOTE] 适用系统
> (centos/rehul)

# ipconfig
```shell
yum -y install net-tools.x86_64
```
# vim
```shell
yum -y install vim
```
# weget
```shell
yum -y install wget
```
# git
```shell
yum -y install git
git config --global credential.helper store //全局保存用户凭据
git config --global user.name bg
git config --global user.email bzqwangyi2017@163.com
```

# docker
1. 安装依赖 
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
2. 安装对应镜像源(华为)
```shell
wget -O /etc/yum.repos.d/docker-ce.repo https://mirrors.huaweicloud.com/docker-ce/linux/centos/docker-ce.repo
```
3. 修改镜像源地址
```shell
sudo sed -i 's/download.docker.com/mirrors.huaweicloud.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo 
```
4. 更新索引文件并安装
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
5. 启动docker

```sh
systemctl start docker

systemctl enable docker   //开机自启

docker run hello-world    /Helloword 测试安装成功
```
6. 配置docker国内镜像源
```
cd /etc/docker/
vim /etc/docker/daemon.json
```
```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://docker.m.daocloud.io",
    "https://docker.xuanyuan.me",
    "https://docker.anyhub.us.kg",
    "https://dockerhub.jobcher.com",
    "https://dockerhub.icu"
  ]
}
```
7. 重启docker服务
```sh
sudo systemctl daemon-reload
sudo systemctl restart docker

```

8. 给用户增加docker用户组
```sh
sudo groupadd docker
sudo usermod -aG docker bg // bg是当前用户
newgrp docker //切换用户组, 重启shell
```