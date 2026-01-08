
> [!NOTE] 适用系统
> (centos/rehul)

ipconfig
```shell
yum -y install net-tools.x86_64
```
vim
```shell
yum -y install vim
```
weget
```shell
yum -y install wget
```
git
```shell
yum -y install git
git config --global credential.helper store //全局保存用户凭据
git config --global user.name bg
git config --global user.email bzqwangyi2017@163.com
```

docker
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
sudo yum install docker-ce
```