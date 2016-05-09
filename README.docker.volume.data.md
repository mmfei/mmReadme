数据卷

数据卷是特别设计的目录，绕过了容器的Union File System，向容器提供持久化数据和共享数据的能力。

数据卷可以多个容器共享和重用
数据卷独立于容器存在
更新容器镜像，不影响数据卷
数据卷的读写是直接的，绕过容器的Union File System 例子：

$ docker run -t -i -v /test centos:latest bash
$ docker run -t -i -v /home/test:/home/test centos:latest bash
$ docker run -t -i -v /home/test/data.txt:/home/test/data.txt centos:latest bash
数据卷容器


$ docker run -d -v /data/ --name dbdata centos:latest bash
$ docker run -d --volume-from dbdata --name app centos:latest app
备份 , 挂一个本地地址到新的镜像 , 这个镜像也挂数据卷
docker run -rm --volumes-from dbdata -v $(pwd):/backup busybox tar cvf /backup/backup.tar /data


$ docker run --volumes-from dbdata -v $(pwd):/backup busybox tar xvf /backup/backup.tar

