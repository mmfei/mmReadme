#uwsgi

##日志位置

/data1/logs/app/uwsgi/....log

##启动:
uwsgi.2.0.9 -x /data1/config/uwsgi/flask_mmfei_cn_config.xml --pidfile /tmp/uwsgi.flask.mmfei.cn.pid --stats 127.0.0.1:11002 --daemonize /data1/logs/apps/uwsgi/flask.mmfei.cn.log;

##重启
uwsgi --reload /tmp/uwsgi.flask.mmfei.cn.pid

##杀死
killall -9 uwsgi.2.0.9

##监控
uwsgitop :1717
