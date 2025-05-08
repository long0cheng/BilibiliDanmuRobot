### 本项目概述
    本项目是基于github.com/k-si/bilibili_live项目二开完成
### 使用教程
[点此访问使用教程](https://www.yuque.com/yuqueyonghu3xsgin/igligh/rpr4oslh4nwt2pwv?singleDoc#)
### 功能列表
- [x] 弹幕欢迎（普通用户，舰长用户）
    - [x] 指定用户欢迎
    - [x] 荣耀等级欢迎
    - [x] 分时段欢迎词
    - [x] 自定义欢迎词
    - [x] 欢迎黑名单（模糊匹配，精准匹配）
- [x] 关注答谢
- [x] 分享感谢
- [x] 下播公告
- [x] 礼物答谢
    - [x] 自定义礼物答谢延迟
    - [x] 盲盒统计
- [x] AI机器人
    - [x] 两个ai机器人接口
    - [x] `@帮助`查看机器人触发关键字
- [x] PK相关
    - [x] PK输出对手信息
    - [x] 对方用户串门识别
- [x] 秒级定时弹幕
- [x] 自动更新（GUI）
- [x] 弹幕指令控制
### Docker
# 创建配置文件
```bash
mkdir -p <your path>/etc
```
```bash
wget -O <your path>/etc/bilidanmaku-api.yaml  https://github.moeyy.xyz/https://raw.githubusercontent.com/xbclub/BilibiliDanmuRobot/master/etc/bilidanmaku-api.yaml
```
# 启动容器
```bash
docker run -itd --name bilibilidanmurobot --restart=always -v <your path>:/app/data xbclub/bilibilidanmurobot:latest
```
# 扫码登录
```bash
docker logs bilibilidanmurobot
```
###  构建环境
 * golang version 1.21+
### 构建指令

# 获取构建依赖
```bash
 go mod download
```
 # 构建软件
```bash
 go build cli/bilidanmaku.go
```
#### linux使用musl工具链编译musl全静态可执行文件指令
##### 以下以x64为例

# 指定编译工具链，可通过https://musl.cc/下载
```bash
export CC=/home/user/下载/x86_64-linux-musl-native/bin/gcc
```
```bash
export CXX=/home/user/下载/x86_64-linux-musl-native/bin/g++
```
```bash
export CFLAGS="-I/home/user/下载/x86_64-linux-musl-native/include"
```
```bash
export LDFLAGS="-I/home/user/下载/x86_64-linux-musl-native/lib -Wl,-Bstatic"
```
# 禁用 Cgo，避免引入动态库
```bash
export CGO_ENABLED=0 
```
```bash                                     
export GOOS=linux
```
# 指定编译架构
```bash
export GOARCH=amd64
```
 # 获取构建依赖
```bash
 go mod download
 ```
 # 构建软件
```bash
 go build cli/bilidanmaku.go
```
### Docker编译环境

docker go镜像： golang:1.24-alpine

二进制编译部分
# clone 仓库
```bash
git clone https://github.com/xbclub/BilibiliDanmuRobot.git
```
#拉取依赖
```bash
cd BilibiliDanmuRobot
```
```bash
go mod tidy
```
# 编译产出物
```bash
GOOS=linux GOARCH=你所需架构 go build -v -o BilibiliDanmuRobot -ldflags "-X main.Version=GIT TAG的版本号（可以自定义）" --trimpath
```
构建docker 镜像
注意构建镜像需要二进制本体重命名为app，并将app二进制文件和etc文件夹放入app/data 目录，目录结构为 app/app ,
运行时需要将文件夹挂载入docker容器的 /app/data 目录，并且需要将etc文件夹放入挂载目录中,最终结构为 app/app,app/data/etc
```
from alpine

run sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories && apk add --no-cache tzdata
copy app /app
run mkdir /app/data
workdir /app/data
ENTRYPOINT ["/app/BilibiliDanmuRobot"]
```
运行容器
# 创建配置文件
```bash
mkdir -p <your path>/etc
```
```
wget -O <your path>/etc/bilidanmaku-api.yaml  https://github.moeyy.xyz/https://raw.githubusercontent.com/xbclub/BilibiliDanmuRobot/master/etc/bilidanmaku-api.yaml
```
# 启动容器
```bash
docker run -itd --name bilibilidanmurobot --restart=always -v <your path>:/app/data xbclub/bilibilidanmurobot:latest
```
# 扫码登录
```
docker logs bilibilidanmurobot
```
### 鸣谢
- github.com/k-si/bilibili_live
