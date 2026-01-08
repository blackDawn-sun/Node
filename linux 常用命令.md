# yum
```shell
yum repolist //查所有yum源地址
yum repolist --verbose | grep <repository-id> //查yum仓库id具体的信息,url地址
ls /etc/yum.repos.d/ //列出所有yum源
```
# 查版本号
```shell
cat /etc/os-release 
uname -a
```
```shell
[root@aos01 ~]# cat /etc/os-release
NAME="Anolis OS"
VERSION="8.10"
ID="anolis"
ID_LIKE="rhel fedora centos"   // rhel 红帽
VERSION_ID="8.10"
PLATFORM_ID="platform:an8"
PRETTY_NAME="Anolis OS 8.10"
ANSI_COLOR="0;31"
HOME_URL="https://openanolis.cn/"
```
# 修改主机名
```
# 查看当前主机名
hostnamectl

# 修改主机名（将"new-hostname"替换为实际名称）
sudo hostnamectl set-hostname new-hostname

sudo systemctl restart systemd-hostnamed //手动生效(无需重启,但要刷新ssh连接)

#检测生效(是否存在未修改的地方)
cat /etc/hostname
cat /etc/hosts
```
# 修改主机ip
1. 进入文件夹/etc/sysconfig/network-scripts
```sh
cd /etc/sysconfig/network-scripts
```
2. 修改文件夹下网络配置文件(如 ifcfg-ens160)
```sh
[root@aos02 network-scripts]# cat ifcfg-ens160 
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=eui64
NAME=ens160
UUID=c9de205b-1016-4ba7-a83b-0260963f4037
DEVICE=ens160
ONBOOT=yes
IPADDR=192.168.100.102
PREFIX=24
GATEWAY=192.168.100.2
DNS1=192.168.100.2
```
翻译对照表
```
TYPE="Ethernet"：指定网络接口的类型为以太网。  
PROXY_METHOD="none"：表示不使用代理方法。  
BROWSER_ONLY="no"：表示该接口不仅用于浏览器，还可以用于其他应用程序。  
BOOTPROTO="dhcp"：指定网络接口的IP地址获取方式为动态主机配置协议（DHCP）。静态IP设置为static  
DEFROUTE="yes"：表示该接口是默认路由。  
IPV4_FAILURE_FATAL="no"：表示如果IPv4配置失败，系统不会终止启动过程。  
IPV6INIT="yes"：表示启用IPv6初始化。  
IPV6_AUTOCONF="yes"：表示启用IPv6自动配置功能。  
IPV6_DEFROUTE="yes"：表示将该接口设置为IPv6默认路由。  
IPV6_FAILURE_FATAL="no"：表示如果IPv6配置失败，系统不会终止启动过程。  
IPV6_ADDR_GEN_MODE="stable-privacy"：表示IPv6地址生成模式为稳定隐私模式。  
NAME="ens33"：指定网络接口的名称为ens33。  
UUID="b739149b-321c-400f-bb4a-63e030896119"：为网络接口分配一个唯一的标识符。  
DEVICE="ens33"：指定网络接口的设备名称为ens33。  
ONBOOT="yes"：表示在系统启动时自动激活该网络接口
```
3. 修改ip,子网掩码之类
4. 重启



# 结尾




