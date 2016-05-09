pip install virtualenvwrapper;

#配置
echo "export WORKON_HOME=/data1/pythonWorkspace" >> ~/.bashrc;
export WORKON_HOME=/data1/pythonWorkspace;

#切换环境
source /usr/bin/virtualenvwrapper.sh;

#创建环境
mkvirtualenv env2;

#列出环境:
lsvirtualenv -b

#切换环境
workon env1
#校验环境
echo $VIRTUAL_ENV


#查看环境安装了什么包:
lssitepackages

#进入当前环境的目录：cdvirtualenv

#删除环境 rmvirtualenv env2


#由于自己的mac环境有问题 , 就用下面的方式切换到管理环境吧.....我自己都觉得雷倒了
. /data1/htdocs/flask.mmfei.cn/mm/bin/activate;VIRTUALENVWRAPPER_PYTHON=/data1/htdocs/flask.mmfei.cn/mm/bin/python2;source /usr/local/bin/virtualenvwrapper.sh;
