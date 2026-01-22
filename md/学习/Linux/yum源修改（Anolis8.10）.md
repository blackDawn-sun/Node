> 参考： [Site Unreachable](https://zhuanlan.zhihu.com/p/1900572499286139768)

### 备份当前yum源
```sh
mkdir /etc/yum.repos.d/backup
mv /etc/yum.repos.d/*.repo /etc/yum.repos.d/backup/
```
### 编辑 YUM 仓库配置文件

```sh
vi /etc/yum.repos.d/Anolis8.10.repo
```
修改内容

```



```bash
[base]
name=Anolis-$releasever - Base - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/BaseOS/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/BaseOS/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/BaseOS/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS
 
[AppStream]
name=Anolis-$releasever - AppStream - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/AppStream/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/AppStream/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/AppStream/$basearch/os/
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS
 
[DDE]
name=Anolis-$releasever - DDE - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/os/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/os/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/os/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS
 
[Devel]
name=Anolis-$releasever - Devel - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/Devel/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/Devel/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/Devel/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[Experimental]
name=Anolis-$releasever - Experimental - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/Experimental/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/Experimental/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/Experimental/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[Extras]
name=Anolis-$releasever - Extras - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/Extras/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/Extras/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/Extras/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[HighAvailability]
name=Anolis-$releasever - HighAvailability - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/HighAvailability/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/HighAvailability/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/HighAvailability/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[NDE]
name=Anolis-$releasever - NDE - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/NDE/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/NDE/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/NDE/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[Plus]
name=Anolis-$releasever - Plus - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/Plus/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/Plus/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/Plus/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[PowerTools]
name=Anolis-$releasever - PowerTools - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/PowerTools/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/PowerTools/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/PowerTools/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS

[kernel-5.10]
name=Anolis-$releasever - isos - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/anolis/$releasever/kernel-5.10/$basearch/os/
        http://mirrors.aliyuncs.com/anolis/$releasever/kernel-5.10/$basearch/os/
        http://mirrors.cloud.aliyuncs.com/anolis/$releasever/kernel-5.10/$basearch/os/
gpgcheck=1
enabled=1
gpgkey=https://mirrors.aliyun.com/anolis/RPM-GPG-KEY-ANOLIS
```

```bash
# 因为上面的基础源无法下载pssh这个常用软件，我只能去扒阿里的epel源里的东西了
# 百度一下就知道，龙蜥8.10对应的是redhat8版本
[Everything]
name=Extra Packages for Enterprise Linux 8 - $basearch
baseurl=http://mirrors.aliyun.com/epel/8/Everything/$basearch
failovermethod=priority
enabled=1
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/epel/RPM-GPG-KEY-EPEL-8

[Modular]
name=Extra Packages for Enterprise Linux 8 - $basearch - Modular
baseurl=http://mirrors.aliyun.com/epel/8/Modular/$basearch/
failovermethod=priority
enabled=1
gpgcheck=1
gpgkey=https://mirrors.aliyun.com/epel/RPM-GPG-KEY-EPEL-8
```
### 清理缓存并更新 YUM 数据库

修改完配置后，你需要清理 YUM 的缓存并更新 YUM 数据库，以确保新的仓库设置生效。
```sh
yum clean all 
yum makecache
```