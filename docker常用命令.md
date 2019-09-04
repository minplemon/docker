## 镜像中 安装插件
这个命令会在docker容器中执行"apt-get install -y ping"，也就是安装一个ping命令，运行完之后容器就自动退出了
```
docker run ddfddf/tutorial apt-get install -y ping
docker commit 0299878039f0 ddfddf/ping  #0299878039f0 通过 docker ps -a 查找
```
## 复制文件到本地
```
docker cp [OPTIONS] [CONTAINER_ID]:[SRC_PATH] [DEST_PATH]
docker cp mynginx:/etc/nginx /etc/nginx
```
## 复制文件到镜像
```
docker cp /etc/nginx mynginx:/etc/nginx
```

## 从 container 创建 image
```
- 命令
  docker commit [container] [imageName]
- 实例
docker commit nginx king101125s/nginxStudy:v1
```

## push images到hub.docker.com
```
- 命令
  docker push usename/repository:TAG
- 实例
  docker push king101125s/nginxStudy:v1
```
