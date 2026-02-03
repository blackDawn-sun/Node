
安装pyinstaller
```sh
pip install pyinstaller
```
安装pillow 解决ico格式不对，png之类格式可以默认转为ico图标
```sh
pip install pillow
```
打包

```sh
#
pyinstaller -F -i 1.ico --add-data "resource;resource" win.py
```