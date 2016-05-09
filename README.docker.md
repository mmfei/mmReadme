boot2docker start
boot2docker download
boot2docker stop

#-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上， -i 则让容器的标准输入保持打开。
sudo run -t -i centos /bin/bash



Install Docker Toolbox using instructions at: http://docs.docker.com/installation/mac/
Start Docker Toolbox from the command line and run: 
```
docker-machine create -d virtualbox dev
```
Get your Docker IP address with: 
```
    docker-machine ip dev
```
Use sudo nano /etc/hosts to add <Docker IP> dockerhost to your /etc/hosts file
Run: 
```
docker-machine env dev
```
and copy the export statements to your ~/.bash_profile by running sudo nano ~/.bash_profile. Then run: source ~/.bash_profile
Run: 
```
docker run --name mattermost-dev -d --publish 8065:80 mattermost/platform
```
When docker is done fetching the image, open 
http://dockerhost:8065/ in your browser.




# 创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。
docker-machine create --engine-registry-mirror=https://i8sz98df.mirror.aliyuncs.com -d virtualbox ali 

# 查看机器的环境配置，并配置到本地。然后通过Docker客户端访问Docker服务。
docker-machine env ali
eval "$(docker-machine env ali)"
docker info

#查看设备的配置
docker-machine inspect ali
#docker-machine start ali
#http://192.168.99.101:8065/ssssd/channels/off-topic
```
 export DOCKER_TLS_VERIFY="1"
 export DOCKER_HOST="tcp://192.168.99.101:2376"
 export DOCKER_CERT_PATH="/Users/mmfei/.docker/machine/machines/ali"
 export DOCKER_MACHINE_NAME="ali"
```


```
#/etc/sysconfig/docker 
#other_args=-bip=192.168.100.1/24

#install
docker run --name mattermost-dev -d --publish 8065:80 mattermost/platform

#start
docker start mattermost-dev
#stop
docker stop mattermost-dev
#delete
#docker rm -v mattermost-dev
#ssh
docker exec -ti mattermost-dev /bin/bash



#nginx config
upstream mattermost_proxy {
  server 127.0.0.1:8065;
}

server {
  listen       80;
  server_name  mattermost.mmfei.com;

  #ssl on;
  #ssl_certificate      /etc/nginx/ssl/server.crt;
  #ssl_certificate_key  /etc/nginx/ssl/commercial.key;

  #ssl_session_cache shared:SSL:1m;
  #ssl_session_timeout  5m;
  #ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

  location / {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_redirect off;
    proxy_pass http://mattermost_proxy;
  }

  location /api/v1/websocket {
    proxy_pass http://mattermost_proxy;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
  }

  access_log  /data1/logs/web/mattermost.mmfei.com.access.log;
  client_max_body_size 4G;
  keepalive_timeout 10;
}
```
