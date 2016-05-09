只有第9种信号(SIGKILL)才可以无条件终止进程，其他信号进程都有权利忽略。  下面是常用的信号：
HUP    1    终端断线
INT     2    中断（同 Ctrl + C）
QUIT    3    退出（同 Ctrl + \）
TERM   15    终止
KILL    9    强制终止
CONT   18    继续（与STOP相反， fg/bg命令）
STOP    19    暂停（同 Ctrl + Z）
