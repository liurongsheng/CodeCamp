# docker

## 安装包 
[下载地址](https://www.docker.com/products/docker-desktop)

## 命令
- 镜像列表
docker image ls

- 查看 WEB 应用容器
docker ps -a

- 停止一个容器
docker stop <容器 ID>
docker stop 6ac441028a0f

- 重启一个容器
docker restart 5dfc9d7e7e40

- 删除一个容器
docker rm -f 732ceba7908d
docker rm -f 6ac441028a0f

- 删除所有已经停止的容器
docker container prune

- 运行一个 web 应用
runoob@runoob:~# docker pull training/webapp  # 载入镜像
runoob@runoob:~# docker run -d -P training/webapp python app.py
docker run -d -p 80:80 --name docker-image docker-container

-d:让容器在后台运行。
-P:将容器内部使用的网络端口映射到我们使用的主机上。

## 其他命令
docker container ls：默认只列出正在运行的容器，-a 选项会列出包括停止的所有容器。
docker image ls：列出镜像信息，-a 选项会列出 intermediate 镜像(就是其它镜像依赖的层)。
docker volume ls：列出数据卷。
docker network ls：列出 network。
docker info：显示系统级别的信息，比如容器和镜像的数量等

docker container prune # 删除所有退出状态的容器
docker volume prune # 删除未被使用的数据卷
docker image prune # 删除 dangling 或所有未被使用的镜像


## 问题
Error response from daemon: open \\.\pipe\docker_engine_linux: The system cannot find the file specified.
```
cd "C:\Program Files\Docker\Docker"
DockerCli.exe -SwitchDaemon
```

##  aria2-pro

docker run -d \
  --name aria2-pro \
  --restart unless-stopped \
  --log-opt max-size=1m \
  -e PUID=$UID \
  -e PGID=$GID \
  -e RPC_SECRET=<TOKEN> \
  -e RPC_PORT=6800 \
  -p 6800:6800 \
  -e LISTEN_PORT=6888 \
  -p 6888:6888 \
  -p 6888:6888/udp \
  -v ~/aria2-config:/config \
  -v ~/downloads:/downloads \
  p3terx/aria2-pro
  
docker run -d --name aria2-pro --restart unless-stopped --log-opt max-size=1m -e PUID=$UID -e PGID=$GID -e RPC_SECRET=admin123 -e RPC_PORT=6800 -p 6800:6800 -e LISTEN_PORT=6888 -p 6888:6888 -p 6888:6888/udp -v ~/aria2-config:/config -v ~/downloads:/downloads p3terx/aria2-pro

docker run -d --name ariang --log-opt max-size=1m --restart unless-stopped -p 6880:6880 p3terx/ariang

http://token:admin123@localhost:6800/jsonrpc

