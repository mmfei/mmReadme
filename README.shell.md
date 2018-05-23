#查看端口
netstat  -nap  tcp

#top5内存占用
ps -eo rss,pmem,pcpu,args |sort -unrk1 |head -n5

