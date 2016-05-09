STAT pid 22362    //memcache服务器的进程ID
STAT uptime 1469315    //服务器已经运行的秒数
STAT time 1339671194    //服务器当前的unix时间戳
STAT version 1.4.9    //memcache版本
STAT libevent 1.4.9-stable    //libevent版本
STAT pointer_size 64    //当前操作系统的指针大小（32位系统一般是32bit,64就是64位操作系统）
STAT rusage_user 3695.485200    //进程的累计用户时间
STAT rusage_system 14751.273465    //进程的累计系统时间
STAT curr_connections 69    //服务器当前存储的items数量
STAT total_connections 855430    //从服务器启动以后存储的items总数量
STAT connection_structures 74    //服务器分配的连接构造数
STAT reserved_fds 20    //
STAT cmd_get 328806688    //get命令（获取）总请求次数
STAT cmd_set 75441133    //set命令（保存）总请求次数
STAT cmd_flush 34    //flush命令请求次数
STAT cmd_touch 0    //touch命令请求次数
STAT get_hits 253547177    //总命中次数
STAT get_misses 75259511    //总未命中次数
STAT delete_misses 4    //delete命令未命中次数
STAT delete_hits 565730    //delete命令命中次数
STAT incr_misses 0    //incr命令未命中次数
STAT incr_hits 0    //incr命令命中次数
STAT decr_misses 0    //decr命令未命中次数
STAT decr_hits 0    //decr命令命中次数
STAT cas_misses 0    //cas命令未命中次数
STAT cas_hits 0        //cas命令命中次数
STAT cas_badval 0    //使用擦拭次数
STAT touch_hits 0    //touch命令未命中次数
STAT touch_misses 0    //touch命令命中次数
STAT auth_cmds 0    //认证命令处理的次数
STAT auth_errors 0    //认证失败数目
STAT bytes_read 545701515844        //总读取字节数（请求字节数）
STAT bytes_written 1649639749866    //总发送字节数（结果字节数）
STAT limit_maxbytes 2147483648        //分配给memcache的内存大小（字节）
STAT accepting_conns 1            //服务器是否达到过最大连接（0/1）
STAT listen_disabled_num 0    //失效的监听数
STAT threads 4        //当前线程数
STAT conn_yields 14    //连接操作主动放弃数目
STAT hash_power_level 16    //
STAT hash_bytes 524288
STAT hash_is_expanding 0
STAT expired_unfetched 30705763
STAT evicted_unfetched 0
STAT bytes 61380700    //当前存储占用的字节数
STAT curr_items 28786    //当前存储的数据总数
STAT total_items 75441133    //启动以来存储的数据总数
STAT evictions 0    //为获取空闲内存而删除的items数（分配给memcache的空间用满后需要删除旧的items来得到空间分配给新的items)
STAT reclaimed 39957976    //已过期的数据条目来存储新数据的数目
