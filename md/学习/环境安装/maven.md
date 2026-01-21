#maven #mvn 
## 官网下载 
>官网下载地址：[Download Apache Maven – Maven](https://maven.apache.org/download.cgi)
>maven历史版本下载入口： [Apache Archive Distribution Directory](https://archive.apache.org/dist/maven/maven-3/)

历史版本入口

![](assets/maven/file-20260121120924686.png)
查找对应版本地址
![](assets/maven/file-20260121121042925.png)
![](assets/maven/file-20260121121013495.png)
## 设置本地仓库地址
conf/settings.xml: (地址自定义，文中以D:\myspace\KF\KF-Environment\maven\repo 为例)
```xml
    <localRepository>D:\myspace\KF\KF-Environment\maven\repo</localRepository>
```

## 修改镜像地址
conf/settings.xml:
```xml
<mirrors>
    <mirror>
        <id>aliyunmaven</id>
        <name>阿里云公共仓库</name>
        <url>https://maven.aliyun.com/repository/public</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
</mirrors>
```
## 配置环境变量
