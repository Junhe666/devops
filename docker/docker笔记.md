
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

查看容器进程

docker top可以查看运行容器中运行的进程 
一般用于查看后台型，交互型的需要到其他终端下查看 
首先创建一个后台型容器并处于始终睡眠 
``
docker run -d --name=daemon_top ubuntu /bin/bash -c 'while true;do sleep 1;done;'
 
docker ps查看一下运行的容器 
docker top daemon_top将看到如下
 
UID PID PPID C STIME TTY TIME CMD 
root 22858 22848 0 22:10 ? 00:00:00 /bin/bash -c while true;do sleep 1; done 
root 22915 22858 0 22:10 ? 00:00:00 sleep 1 
``
这里能看到两个进程while和sleep（这里我听说shell中的一条语句就是一个进程？？不知道是不是真的，下次可以试试？？？）

查看容器信息

docker inspect 容器名/容器ID可以查看容器的配置信息：容器名，环境变量， 运行命令， 主机配置，网络配置，数据卷配置。 
主要还是需要了解这些内容的细节。（这个接下来再具体了解。） 
-f或者–format格式化标识， 
查询容器的运行状态： 
``
docker inspect --format='{{.State.Running}}' 容器名 
``

查询容器的IP的地址 
docker inspect --format='{{.NetworkSettings.IPAddress}}' 容器名

容器内执行命令
我们通常可能会在一个正在运行的容器中启动另一个程序（并发启动）会用到docker exec命令 
执行命令可以创建交互型和后台型
 
-d：后台型 
-it：标准输入和关联终端 

docker exec -d 容器名 touch /tmp/new_file 

这个命令就是要运行一个后台任务，在 
/tmp下创建一个名为new_file的文件 
docker exec -it 容器名 /bin/bash 

这个命令都可以用交互型和后台型容器。 
如果用于后台型容器就可以为后台型容器关联一个终端。 
（这里可以想想前台程序和后台程序的区别？？？？）

容器的导入和导出

docker export命令提供一种容器持久化的方式。我们在运行了容器后修改配置等等操作后，我们用

docker export 命令将容器导出成文件，这样我们就可以进行分享。
 
docker export 容器名 > 文件名 

导出后我们当然也可以将文件导入作为镜像 
cat 文件名 | docker import - 镜像名:标记 

import会将从标准输入 读取容器内容。 

import也可以从网络上导入容器 

docker import url res:tag(镜像名：标记) 

思考？？？ 
res:tag具体对应什么可以去找一个例子试试。