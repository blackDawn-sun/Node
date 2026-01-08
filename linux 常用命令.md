yum
```shell
yum repolist //查所有yum源地址
yum repolist --verbose | grep <repository-id> //查yum仓库id具体的信息,url地址
ls /etc/yum.repos.d/ //列出所有yum源
```
查版本号
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


