#electron 
## 原生html方式 快速启动

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
    "test": "echo \"Error: no test specified\" && exit 1"  },  
  "author": "BG",  
  "license": "ISC",  
  "devDependencies": {  
    "electron": "^40.6.1"  
  }  
}
```

### 2. 安装electron
#安装electron
```sh
npm install electron --save-dev
```
淘宝镜像源安装失败方法
先执行
```sh
npm config edit
```
修改弹出的配置文件.npmrc
```
registry=https://registry.npmmirror.com
electron_mirror=https://cdn.npmmirror.com/binaries/electron/
electron_builder_binaries_mirror=https://npmmirror.com/mirrors/electron-builder-binaries/
```
如图
![](assets/electron/file-20260304103738747.png)
删除你项目的node_modules文件夹
重启cmd命令行工具（vscode或者其他ide也要重启一下，更稳妥）
执行下面命令清除npm的缓存
```sh
npm cache clean --force
```
问题已经解决了，再执行命令安装electron试试
```sh
npm install electron --save-dev
```
> 参考：[electron安装报错终极解决办法\_npm install electron报错-CSDN博客](https://blog.csdn.net/oNuoZuo/article/details/140712310?spm=1001.2014.3001.5502)

### 3.package.json添加start
package.json
```json
{  
  "name": "wsjy",  
  "version": "1.0.0",  
  "description": "WSJY DOWNLOAD",  
  "main": "main.js",  
  "scripts": {  
    "start": "electron .",  
    "test": "echo \"Error: no test specified\" && exit 1"  },  
  "author": "BG",  
  "license": "ISC",  
  "devDependencies": {  
    "electron": "^40.6.1"  
  }  
}
```
### 4.创建main.js文件
main.js
```js
const {app, BrowserWindow} = require('electron')  
  
function createWindow(){  
    const win =  new BrowserWindow({  
        width: 800,  
        height: 600,  
        autoHideMenuBar: true  //关闭菜单栏
    })  
   // win.loadFile("./pages/index.html")
    win.loadURL('https://www.douyin.com/')  
  
}  
  
// == 关键 == 可用 app.whenReady().then(() => {}) 
app.on('ready', ()=>{  
    createWindow()  
  
    // 兼容苹果系统，应用激活时创建窗口  （可选）
    app.on('activate', () => {  
        if (BrowserWindow.getAllWindows().length === 0) createWindow()  
    })  
})  
  
// 兼容window 所有窗口关闭时，程序结束  （可选）
app.on('window-all-closed', () => {  
    if (process.platform !== 'darwin') app.quit()  
})
```
### 5.启动
```sh
npm start
```
### 6. 添加内容安全策略（可选）
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src https://*; child-src 'none';" />
```
### 7. 热部署（可选）
安装nodemon
```sh
npm i nodemon
```
修改package.json start 为nodemon --exec electron .
```
{  
  "name": "wsjy",  
  "version": "1.0.0",  
  "description": "WSJY DOWNLOAD",  
  "main": "main.js",  
  "scripts": {  
    "start": "nodemon --exec electron .",  
    "test": "echo \"Error: no test specified\" && exit 1"  },  
  "author": "BG",  
  "license": "ISC",  
  "devDependencies": {  
    "electron": "^40.6.1"  
  },  
  "dependencies": {  
    "nodemon": "^3.1.14"  
  }  
}
```
项目文件夹下增加nodemon.json配置
```json
{  
  "ignore": [  
    "node_modules",  
    "dist"  
  ],  
  "watch": [  
    "*",  
    "*"  
  ],  
  "ext": "html,js,css",  
  "restartable": "r"  
}
```
## 预加载脚本

### 预加载脚本使用
例如将node脚本信息传到渲染进程里
主进程main.js 
增加webPreferences 配置
```js
const {app, BrowserWindow} = require('electron')  
const path = require("node:path");  

function createWindow(){  
    const win =  new BrowserWindow({  
        width: 800,  
        height: 600,  
        autoHideMenuBar: true, //关闭菜单栏  
        webPreferences: {  
            preload: path.join(__dirname, 'preload.js')  //填绝对地址
        }  
    })  
  
    // win.loadURL('https://www.douyin.com/')  
    win.loadFile("./pages/index.html")  
  
}  
  
// == 关键 == 可用 app.whenReady().then(() => {})
app.on('ready', ()=>{  
    createWindow()  
  
    // 兼容苹果系统，应用激活时创建窗口  
    app.on('activate', () => {  
        if (BrowserWindow.getAllWindows().length === 0) createWindow()  
    })  
})  
  
// 兼容window 所有窗口关闭时，程序结束  
app.on('window-all-closed', () => {  
    if (process.platform !== 'darwin') app.quit()  
})
```
预加载脚本 项目位置/preload.js
preload.js
```js
// node 版本  
console.log("preload",process.version);  
const {contextBridge} = require('electron');  
contextBridge.exposeInMainWorld('myApi',{  
    version:process.version
})
```
渲染进程
js
```js
const btn1 = document.getElementById("btn1");  

btn1.onclick = function(){  
  
    alert(myApi.version);  
}  

```
html
```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>hello</title>  
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src https://*; child-src 'none';" />  
  
</head>  
<body>  
<h1>  
    hello,word!  
    <button id="btn1"> 点我 </button>  

    <script src="./js/index.js"></script>  
</h1>  
</body>  
</html>
```


### 渲染进程=》（预加载脚本）=》主进程

#### 预加载脚本preload.js
ipcRenderer,ipcRenderer.send
```js
// node 版本  
console.log("preload",process.version);  
const {contextBridge,ipcRenderer} = require('electron');  
contextBridge.exposeInMainWorld('myApi',{  
    version:process.version,  
    mysave:(value)=>{  
        ipcRenderer.send("file-value", value);  
    }  
})
```
#### 渲染进程
js
```js
const btn1 = document.getElementById("btn1");  
const user = document.getElementById("user");  
const btn2 = document.getElementById("btn2");  
  
btn1.onclick = function(){  
  
    alert(myApi.version);  
}  
  
btn2.onclick = function(){  
    myApi.mysave(user.value);  
}
```
html
```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>hello</title>  
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src https://*; child-src 'none';" />  
  
</head>  
<body>  
<h1>  
    hello,word!  
    <button id="btn1"> 点我 </button>  
       <br>    <br>    输入内容：  
    <input type="text" id="user">  
    <button id="btn2">写入文件</button>  

    <script src="./js/index.js"></script>  
</h1>  
</body>  
</html>
```
#### 主进程
ipcMain,ipcMain.on
```js
const {app, BrowserWindow,ipcMain} = require('electron')  
const path = require("node:path");  
const fs = require('fs');  //写入文件 node api
  
  
function saveFile(event,data){  
    fs.writeFileSync("d://hellow.txt", data)  
}  
  
function createWindow(){  
    const win =  new BrowserWindow({  
        width: 800,  
        height: 600,  
        autoHideMenuBar: true, //关闭菜单栏  
        webPreferences: {  
            preload: path.join(__dirname, 'preload.js')  
        }  
    })  
  
    ipcMain.on('file-value', saveFile)  
  
  
    // win.loadURL('https://www.douyin.com/')  
    win.loadFile("./pages/index.html")  
  
}  
  
// == 关键 == 可用 app.whenReady().then(() => {})app.on('ready', ()=>{  
    createWindow()  
  
    // 兼容苹果系统，应用激活时创建窗口  
    app.on('activate', () => {  
        if (BrowserWindow.getAllWindows().length === 0) createWindow()  
    })  
})  
  
// 兼容window 所有窗口关闭时，程序结束  
app.on('window-all-closed', () => {  
    if (process.platform !== 'darwin') app.quit()  
})
```
### 主进程=》（预加载脚本）=》渲染进程
