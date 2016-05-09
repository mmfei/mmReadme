docker run -d -p 5000:5000 registry
docker tag centos 192.168.59.104:5000/centos
docker push 192.168.59.104:5000/centos
