#nodejs #nvm
>nvm是node的版本管理工具，可以方便地安装&切换不同版本的node
## 下载
> 官网下载地址： [GitHub - coreybutler/nvm-windows: A node.js version management utility for Windows. Ironically written in Go.](https://github.com/coreybutler/nvm-windows)
![](assets/nvm/file-20260121143939718.png)
## 安装
解压zip ,执行exe

## 检查安装是否成功

```
nvm -v 
nvm install 12.16.3 
nvm ls 
nvm current 
nvm use 12.16.3 
node -v
```

## 设置npm镜像源
```sh
npm config set registry https://registry.npm.taobao.org/
npm config get registry

#回退默认值：
npm config set registry https://registry.npmjs.org/

#其他镜像源
#华为
npm config set registry https://mirrors.huaweicloud.com/repository/npm/ 
npm cache clean -f
```

## ~~设置nodejs源地址（已废弃）~~
```sh
#华为源
npm config set disturl https://mirrors.huaweicloud.com/nodejs
```

