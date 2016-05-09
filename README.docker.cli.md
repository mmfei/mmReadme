docker run -ti centos /bin/bash
docker ps 列出容器
docker logs 显示容器的标准输出
docker stop 停止正在运行的容器

eval $(docker-machine env default);
docker run -ti centos /bin/bash;



# docker-machine create --engine-registry-mirror=https://i8sz98df.mirror.aliyuncs.com -d virtualbox default


#docker rm $(docker ps -a | grep -v b95c0bc42aa3 | grep -v docker-registry | awk '{print $1" "$NF}' | grep -v CONTAINER | awk '{print $1}')


docker run -dti -v /Users/mmfei/docker/volume/data/software/tarball:/data1/software/tarball:rw --name mmfei_centos_data_software -h mmfei_centos_data_software fx/centos /bin/bash
docker run -dti -v /Users/mmfei/docker/volume/data/htdocs:/data1/htdocs:rw --name mmfei_centos_data_htdocs -h mmfei_centos_data_htdocs fx/centos /bin/bash

docker run -dti --volumes-from=mmfei_centos_data_htdocs --volumes-from=mmfei_centos_data_software --name centos.init -h centos.init fx/centos /bin/bash;
