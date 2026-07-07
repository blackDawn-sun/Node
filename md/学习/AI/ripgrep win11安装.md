## PowerShell winget安装
执行命令
```sh
winget install BurntSushi.ripgrep.MSVC
```
## 问题1：
```
Failed when searching source: winget
An unexpected error occurred while executing the command:
0x8a15000f : Data required by the source is missing
```
> 通常是因为 `winget` 的源未正确配置或相关组件缺失导致的

解决方案
```
winget source update
```

## 问题2
```sh
PS C:\Users\JGU7> winget source update
Updating all sources...
Updating source: msstore...
Done
Updating source: winget...
Cancelled
Updating source: winget-font...
Cancelled
```
> 从您的输出来看，`winget` 在尝试更新默认的 `winget` 源时失败了（状态显示为 `Cancelled`），这通常是因为连接微软官方源的网络不稳定或超时导致的。

为了彻底解决这个问题并让 `winget` 恢复正常，**强烈建议您将 `winget` 的源替换为国内镜像**（如南京大学、中国科学技术大学等）。国内镜像速度快且稳定，可以完美避开官方源连接失败的问题
解决方法：
1.  移除默认的官方源
```sh
winget source remove winget
```
2. 添加国内镜像源
```sh
winget source add winget https://mirror.nju.edu.cn/winget-source --trust-level trusted
```
3. 更新源并验证
```
winget source update
```
## 问题3
```
An unexpected error occurred while executing the command: 0x80072f7d : unknown error
```
这个 `0x80072f7d` 错误通常与网络连接、SSL/TLS 证书问题或防火墙拦截有关。由于 `winget` 依赖微软的服务器，国内网络环境或安全软件很容易导致此类连接失败
解决方法
某些网络环境（如使用网银插件后）可能会导致 TLS 1.2 或 1.3 协议被意外关闭。

1. 按 `Win + R` 键，输入 `inetcpl.cpl` 回车，打开“Internet 属性”。
2. 切换到“高级”选项卡，向下滚动找到“安全”部分。
3. 确保勾选了 **使用 TLS 1.2** 和 **使用 TLS 1.3**（如果有的话）。
4. 点击“应用”并“确定”