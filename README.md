## golang SSH客户端三件套
go ssh相关的demo
- 远程登录
- 端口映射
- 文件传输
## 准备一台远程主机
可以使用alpinessh快速创建一个ssh主机，项目地址：https://github.com/basicimage/alpinessh
```bash
docker run -d -p 222:22 --rm bimg/alpinessh
# 默认账号密码 root:123456
```
## 远程登录
```bash
go run terminal.go
```
可以看到，直接进入主机命令界面，为了方便后面的操作，我们在主机内装一个nginx
```bash
apk add nginx
nginx #启动nginx
```
## 端口映射
```bash
go run forward.go
```
注意要在本项目目录新启动一个命令行界面，不要在上面远程命令行界面操作
```bash
curl http://localhost:8800 
```
返回页面为404，说明端口映射成功
## 文件传输
```bash
go run sftp.go
```
把`default.conf`(nginx配置)和`index.html`上传上去，再远程命令行重启`nginx`
```bash
nginx -s reload
curl http://localhost:8800 
```
可以看到，返回我们自定义的页面了。

### ps:
定义成`/tmp`目录主要是权限问题

这里也会把远程的`/bin/bash`文件下载下来。