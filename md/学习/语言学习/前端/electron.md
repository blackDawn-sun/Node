#electron 
## 原生html方式

### 1. 创建文件夹并初始化
```sh
npm init
```
修改package.json,author，description
```json
{

  "name": "wsjy",

  "version": "1.0.0",

  "description": "WSJY DOWNLOAD",

  "main": "main.js",

  "scripts": {

    "test": "echo \"Error: no test specified\" && exit 1"

  },

  "author": "BG",

  "license": "ISC"

}
```

### 2. 安装electron
```sh
npm install electron --save-dev
```