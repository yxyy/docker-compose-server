
### docker compose 容器集群管理实例

我的`sever`目录结构是：`/usr/local/docker/server`，如果不同，你需要修改`docker-compose.yaml`对应的挂载路径

nginx 配置的项目在 `/data/` 下，这里不提供项目，自己创建测试项目或更改配置指向自己的项目

在保证已安装`docker`和`docker compose`的情况下，直接运行
```shell
docker compose up -d 
```


### 配置文件来源说明

配置文件都是先启动一个临时容器，然后拷贝到出来的

下面是nginx配置示例
```shell
#启动一个 nginx 临时容器
docker run --name tmpnginx -it  -d nginx

#进入容器
docker exec -it tmpnginx /bin/bash

#查找配置文件位置
find / -name nginx.conf

#退出容器，拷贝容器nginx配置
docker cp tmpnginx:/ect/nginx /tmp/nginx

```