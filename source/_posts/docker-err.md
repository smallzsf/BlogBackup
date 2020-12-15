---
title: Docker 容器磁盘占用100%(/var/lib/docker/overlay2空间占用很大)
date: 2020-12-04 10:14:11
tags:
    docker
---

####  首先查看磁盘占用

    df -h

####  结果显示多条如下数据

    overlay  40G   40G  0G  100% /var/lib/docker/overlay2/{id}/merged

####  清理无用的docker数据

    docker system prune -a

#### 清理为none镜像

    $ docker rmi $(docker images | grep "none" | awk '{print $3}')

    $ docker stop $(docker ps -a | grep "Exited" | awk '{print $1 }') //停止容器

    $ docker rm $(docker ps -a | grep "Exited" | awk '{print $1 }') //删除容器

    $ docker rmi $(docker images | grep "none" | awk '{print $3}') //删除镜像

- 执行之后，发现虽然清理了2个多G的数据，但是依旧无法明白为何几个微服务会占用那么多的磁盘空间，于是尝试查找系统中的大文件
```
    find / -type f -size +100M -print0 | xargs -0 du -h | sort -nr # 查找"/"目录下所有大于100M的所有文件
```
- 发现/var/lib/docker/containers/{container_id}/下存在数据较大的*-json.log日志文件，百度发现这是docker容器运行的标准输入日志，遂删除之。项目中已使用-v的方式挂载项目输出日志文件，因此对容器运行日志没有了需求，研究后发现在构建参数的时候可以对标准输入日志大小与数量进行限制，以减少日志文件对存储空间的占用，以下配置分别为日志文件最大容量、最大日志文件数。
```
    docker run ...... --log-opt max-size=10m --log-opt max-file=1
```
- 也可以在docker的配置文件中进行全局修改：新建或修改/etc/docker/daemon.json，添加log-dirver和log-opts参数（daemon.json参数说明：https://www.cnblogs.com/pzk7788/p/10180197.html）
  
```
    {
        "log-driver":"json-file",
        "log-opts": {"max-size":"10m", "max-file":"1"}
    }
```

另外，在查找大文件的扫描结果中，可能有通过-v进行了挂载数据目录的，里面的数据可根据相应的挂载目录找到对应的容器进行清理或设置；也可能有出现许多容器产生的未通过-v挂载的目录/var/lib/docker/overlay2/{id}/merged，即文章开头通过df -h找到的文件（如果一个宿主机存在多个容器，多个容器的数据都位于宿主机的overlay（Filesystem）,而且大小一致），可通过docker inspect {container}中GraphDriver找到}/var/lib/docker/overlay2/{id}中的{id}，进而确定容器进行清理或设置