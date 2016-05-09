cat /etc/services |grep 80

lsof
lsof -i4
sudo netstat -nap tcp
lsof -Pn

mac :   lsof -i:8080
linux : neststat -anltp | grep 8080

#查看当时的tcp连接数
netstat -n | awk '/^tcp/ {++state[$NF]} END{for(key in state) {print key,"\t",state[key]}}'

