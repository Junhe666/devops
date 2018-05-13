
## docker安装
https://docs.docker.com/engine/installation/linux/ubuntulinux/

## Dockerfile使用
>http://seanlook.com/2014/11/17/dockerfile-introduction/

>https://blog.csdn.net/yeasy/article/details/40041707

>https://yeasy.gitbooks.io/docker_practice/content/image/dockerfile/copy.html

## docker本地构建
```
docker build -t your_docker_name .   
-t指定images名称
.表示当前目录
```

## docker run
```
docker run -d -p 8080:8080 \
-e DATABASE_TYPE=mysql \
-e DATABASE_HOST=47.104.210.12 \ 
-e DATABASE_NAME=blog \
-e DATABASE_USERNAME=root \
-e DATABASE_PASSWORD=dxq19930502 \ 
-e SERVER_NAME=47.104.210.12 \
--name myblog blog  
```

***
```
docker run -d  -p 10080:8080 \  
-v /usr/local/tomcat/logs \  
--label aliyun.logs.catalina=stdout \  
--label aliyun.logs.access=/usr/local/tomcat/logs/localhost_access_log.*.txt \  
tomcat 
```
用--name指定了容器的名称，在同一台机器上这是唯一的，-p指定了端口；用-e指定环境变量，用--link容器连接了第一个容器，这样在第二个容器的/etc/hosts文件下会有一条记录表示第一个容器的ip和名称，--label是元数据；用-v指定了卷。

## docker挂载物理盘到docker镜像,启动的时候就要输入,比如

docker run -d -p 8000:80 -v /opt/data:/data ysrc/xunfeng:latest

## 删除docker的images镜像

docker images列出所有images的id,

删除docker rmi -f image_id

## 删除docker的container容器

docker ps -a |grep xxxx列出要删除的cotainer,

docker rm -f container_id

## docker查看容器日志
docker logs -tf container_id

## 进入docker容器的方法
不推荐使用旧的docker attach container_id,使用“docker attach”命令进入container（容器）有一个缺点，那就是每次从container中退出到前台时，container也跟着退出了。

推荐使用docker exec -it containerID /bin/bash,加it的意思是退出container后，container仍然在后台运行.要想退出container时，让container仍然在后台运行着，可以使用“docker exec -it”命令。每次使用这个命令进入container，



## docker运行genymotion
https://hub.docker.com/r/matthewhartstonge/genymotion/


>url:
http://thshaw.blogspot.com/2015/07/running-android-apps-in-docker-using.html

### run android app on docker (ARC)
docker run -it --net host --cpuset-cpus 0 --memory 512mb -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v /home/tom/Downloads:/root/Downloads --device /dev/snd --name arcwelder thshaw/arc_welder

docker run -it --net host --cpuset-cpus 0 --memory 512mb -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v $HOME/Downloads:/root/Downloads --device /dev/snd --name arcwelder thshaw/arc-welder

### modify
docker run -it --net host --cpuset-cpus 0 --memory 512mb -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v /Users/apple/Downloads:/Users/apple/Downloads --device /dev/snd --name hello thshaw/arc-welder

## docker运行mysql
```
docker run -p 3306:3306 --name mymysql -v /home/core/conf/:/etc/mysql/ -e MYSQL_ROOT_PASSWORD=dxq19930502 -d mysql:5.6
-v 把物理机的/home/core/conf/文件夹挂载到docker容器的/etc/mysql/里面
```


## docker 批量删除命令

杀死所有正在运行的容器

``
docker kill $(docker ps -a -q)
``

删除所有已经停止的容器

``
docker rm $(docker ps -a -q)
``

删除所有未打 dangling 标签的镜像

``
docker rmi $(docker images -q -f dangling=true)
``

删除所有镜像

``
docker rmi $(docker images -q)
``

强制删除镜像名称中包含“doss-api”的镜像

``
docker rmi --force $(docker images | grep doss-api | awk '{print $3}')
``