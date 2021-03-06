1 . 编译
go build -gcflags "-N -l" test.go 关闭内联优化,便于输出调试信息

2 . 进入gdb环境
sudo /usr/local/gdb/bin/gdb test   

3 . 载入golang运行时支持
(gdb) source /usr/local/go/src/runtime/runtime-gdb.py

4 . gdb下一些调试命令

(gdb) l main.main    #查看源代码代码

(gdb) b 50            #设置断点

(gdb) info b      #查看断点信息
  Num     Type           Disp Enb Address            What
  1       breakpoint     keep y   0x0000000000002239 in main.main at /Users/kenshin/workspace/gogo/test.go:50

(gdb) run             #运行，直到触发断点中断

(gdb) n           #继续执行下一行

(gdb) s           #进入函数/方法

(gdb) info locals   #查看局部变量ma
    err = {tab = 0x0, data = 0xc2000bdfc0}

(gdb) info args   #查看参数
    s = 0xc2000b6f00
    addr = "0.0.0.0:8000
info args

(gdb) help info   

(gdb) p addr      #打印变量
    6 = "0.0.0.0:8000"

(gdb) c           #继续执行，直到下一个断点

(gdb) whatis s        #查看变量类型
    type = struct github.com/hoisie/web.Server *

(gdb) where/bt        #查看堆栈信息,判断函数调用关系

      #0  net.resolveInternetAddr (net="udp4") at /usr/local/go/src/pkg/net/ipsock.go:164
      #1  in net.ResolveUDPAddr (net="udp4") at /usr/local/go/src/pkg/net/udpsock.go:45
      #2  in main.SocketListen (ip="127.0.0.1") at /Users/kenshin/workspace/gor/test.go:13

(gdb) up          #回到上一层调用函数
      #0  in net.ResolveUDPAddr (net="udp4") at /usr/local/go/src/pkg/net/udpsock.go:45
      #1  in main.SocketListen (ip="127.ma0.0.1") at /Users/kenshin/workspace/gor/test.go:13

(gdb) down            #再进入下一层函数
      #0  net.resolveInternetAddr (net="udp4") at /usr/local/go/src/pkg/net/ipsock.go:164
      #1  in net.ResolveUDPAddr (net="udp4") at /usr/local/go/src/pkg/net/udpsock.go:45
      #2  in main.SocketListen (ip="127.0.0.1") at /Users/kenshin/workspace/gor/test.go:13

(gdb) shell           #输入shell，可以进入到shell，输入exit退出shell回到gdb环境
      bash-3.2# exit



通过gdb也可以看到go定义的数据类型底层的实现机制，例如string类型，可以对应到C里面的一个结构体，结构体包含两个属性str和len。 str是一个指向字符数组的指针，len是这个数组的长度。


(gdb) p r   # r string := "process"
16 = {str = 0x2f0170 "process", len = 7}  
(gdb) p r->  #可以通过`TAB`获得一些提示
len  str
(gdb) p r->str   
17 = (uint8 *) 0x2f0170 "process"
