ctrl + ] //jump
ctrl + T //back
ctrl +i //go
ctrl + o //back

set foldmethod=indent "set default foldmethod"
zi 打开关闭折叠
zv 查看此行
zm 关闭折叠
zM 关闭所有
zr 打开
zR 打开所有
zc 折叠当前行
zo 打开当前折叠
zd 删除折叠
zD 删除所有折叠


1. 折叠方式
可用选项 'foldmethod' 来设定折叠方式：set fdm=*****。
有 6 种方法来选定折叠：
manual           手工定义折叠
indent             更多的缩进表示更高级别的折叠
expr                用表达式来定义折叠
syntax             用语法高亮来定义折叠
diff                  对没有更改的文本进行折叠
marker            对文中的标志折叠
注意，每一种折叠方式不兼容，如不能即用expr又用marker方式，我主要轮流使用indent和marker方式进行折叠。

使用时，用：set fdm=marker 命令来设置成marker折叠方式（fdm是foldmethod的缩写）。
要使每次打开vim时折叠都生效，则在.vimrc文件中添加设置，如添加：set fdm=syntax，就像添加其它的初始化设置一样。

2. 折叠命令
选取了折叠方式后，我们就可以对某些代码实施我们需要的折叠了，由于我使用indent和marker稍微多一些，故以它们的使用为例：
如果使用了indent方式，vim会自动的对大括号的中间部分进行折叠，我们可以直接使用这些现成的折叠成果。
在可折叠处（大括号中间）：
zc      折叠
zC     对所在范围内所有嵌套的折叠点进行折叠
zo      展开折叠
zO     对所在范围内所有嵌套的折叠点展开
[z       到当前打开的折叠的开始处。
]z       到当前打开的折叠的末尾处。
zj       向下移动。到达下一个折叠的开始处。关闭的折叠也被计入。
zk      向上移动到前一折叠的结束处。关闭的折叠也被计入。
