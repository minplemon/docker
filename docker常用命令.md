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

## 参看容器ip
```
$ docker inspect container
```

## 设置mysql密码 (运行mysql(--name 容器名称  -e MYSQL_ROOT_PASSWORD设置初始密码  -p 3307:3306  端口映射，主机端口3307))
```shell
docker run --name mysql8.0.19 -e MYSQL_ROOT_PASSWORD=123456 -p 3307:3306 -d mysql:8.0.19
```

## 设置redis(设置密码只需要加上–requirepass,设置redis持久化 --appendonly yes)
```shell
docker run -d --name redis_rc-alpine -p 6378:6379 redis:rc-alpine --requirepass "123456"
docker run -d --name redis_rc-alpine_persistence -p 6377:6379 redis:rc-alpine --requirepass "123456" --appendonly yes -v $PWD/data:/data
docker run -d --name redis_rc-alpine_persistence_data -p 6376:6379 redis:rc-alpine --requirepass "123456" --appendonly yes -v $PWD/data:/data
```

## 设置rabbitMQ密码
```
docker run -d --name rabbitmq3.7.7 -p 5672:5672 -p 15672:15672 -v `pwd`/data:/var/lib/rabbitmq --hostname myRabbit -e RABBITMQ_DEFAULT_VHOST=my_vhost  -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin df80af9ca0c9
```

## 设置mongo 密码
```shell
docker run -d -p 27018:27017 --name mongodb_4.2_bionic -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=123456 bcef5fd2979d
```

## 创建&运行ActiveMQ容器
```shell script
docker run -d --name activemq_5.15.9_alpine_1 -p 61617:61616 -p 8162:8161 rmohr/activemq:5.15.9-alpine
# admin:admin admin 管理员权限
# user:user user 用户权限
```

## 创建&运行zookeeper容器
```shell script
docker run --privileged=true -d --name zookeeper --publish 2181:2181  -d zookeeper:3.5.6
```

说明：
-d 后台运行容器；
--name 指定容器名；
-p 指定服务运行的端口（5672：应用访问端口；15672：控制台Web端口号）；
-v 映射目录或文件；
--hostname  主机名（RabbitMQ的一个重要注意事项是它根据所谓的 “节点名称” 存储数据，默认为主机名）；
-e 指定环境变量；（RABBITMQ_DEFAULT_VHOST：默认虚拟机名；RABBITMQ_DEFAULT_USER：默认的用户名；RABBITMQ_DEFAULT_PASS：默认用户名的密码）
