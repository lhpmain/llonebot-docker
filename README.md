# LLOneBot-Docker
[DockerHub](https://hub.docker.com/r/mlikiowa/llonebot-docker)

## Information
请注意! 该项目使用应当遵守上游开源库协议与要求，遵守当地法律与规范。

该项目适用于快速将NTQQ Bot托管容器，提供Vnc与NoVnc，以便连接图形界面。

## Support Platform/Arch
- [x] Linux/Amd64
- [x] Linux/Arm64

## Install
1. 安装参考已选方案一与方案二 启动
2. 启动后连接Vnc或者NoVnc 到设置配置Bot
   
## 使用方案（一）快速启动
 ```bash
 sudo docker run -d --name onebot-docker0 -e VNC_PASSWD=vncpasswd -p 3000:3000 -p 5900:5900 -p 6081:6081 -p 3001:3001 -v ${PWD}/LiteLoader/:/opt/QQ/LiteLoader/ lhpmain/llonebot-docker
 ```
其中vncpasswd换成你的VNC密码
或者下载代码中的docker-compose.yml，然后执行

```bash
sudo docker-compose up -d
```
## 使用方案（二）快速配置脚本 实验性
零配置脚本 快速启动

 ```bash
curl https://cdn.jsdelivr.net/gh/LLOneBot/llonebot-docker/fastboot.sh -o fastboot.sh & chmod +x fastboot.sh & sudo sh fastboot.sh
 ```
 ```bash
wget -O fastboot.sh https://cdn.jsdelivr.net/gh/LLOneBot/llonebot-docker/fastboot.sh & chmod +x fastboot.sh & sudo sh fastboot.sh
 ```
## Feat
### 崩溃快速重启
你仅仅需要到设置配置自动登录，保证崩溃时手机QQ不在线即可，其余时间可以使用手机QQ

### 数据固化
暂时忽略 未实现QQ本体数据固化 仅实现LiteLoader包括其所有插件数据固化(按照以上流程启动无须考虑，已自动启用) 无需阅读该条目录 

先完成上面的`快速运行`，保证容器在运行状态

如果之前是docker run运行的，执行

```bash
 sudo docker run -d --name onebot-docker0 -e VNC_PASSWD=vncpasswd -p 3000:3000 -p 5900:5900 -p 6081:6081 -p 3001:3001 -v ${PWD}/LiteLoader/:/opt/QQ/LiteLoader/ lhpmain/llonebot-docker
```

如果之前是docker-compose运行的

```bash
docker-compose up -d
```
## Server Login
### noVNC登陆

浏览器访问`http://服务器IP:6081`，默认密码是`vncpasswd`

### VNC登陆

使用VNC软件登陆`服务器IP:5900`，默认密码是`vncpasswd`


### 修改VNC密码

```bash
sudo docker exec onebot-docker0 sh -c "x11vnc -storepasswd newpasswd /root/.vnc/passwd"
```
其中newpasswd换成你的新密码，立即生效，无需重启容器

## 参考与基础
[LLOneBot/LLOneBot](https://github.com/LLOneBot/LLOneBot)

[yuuki-nya/chronocat-docker](https://github.com/yuuki-nya/chronocat-docker/blob/main/Dockerfile)

## 已知问题与提示
### 1.快速闪退
如果连接反向ws后快速闪退 清空容器数据之后 再次配置先启用上报自身消息 在vnc窗口复制 之前触发机器人的消息 使用机器人账号发送 再正常使用bot
