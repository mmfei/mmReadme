# 启用一个会话
    screen -S mmfei

# 临时退出一个会话(不是销毁)
    ctrl + a , ctrl + d

#  列出正在运行的screen
    screen -ls

    There is a screen on:
        2234.mmfei  (Detached)
        
# 进入会话
    screen -r 2234
    screen -r mmfei  


# 退出会话
    exit
