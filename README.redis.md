/usr/local/redis/src/redis-server
/usr/local/redis/src/redis-cli 连上后输入SHUTDOWN 即可关闭

/usr/local/redis.3.0.6/bin/redis-cli -p 6380
/usr/local/redis.3.0.6/bin/redis-server /usr/local/redis.3.0.6/redis.conf
killall -9 redis-server 重启
