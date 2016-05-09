繁星活跃
http://gitlab.fxwork.cn/fanxing/bi2fanxing

#新增活跃留存统计
fx_enterroom
http://gitlab.fxwork.cn/analyze/fxenterroom


#视频延时统计
http://gitlab.fxwork.cn/analyze/fx-ptmconsuming

#kafka -> 文件
kg.postevent
http://gitlab.fxwork.cn/analyze/kafka2file

#kugou7 拉取结果统计
http://gitlab.fxwork.cn/analyze/kg7_log/tree/master/src/kg7.tb.sync
http://biserver.kugou.com/kugou7/ => 


# 粉丝DAU说明
http://gitlab.fxwork.cn/fanxing/bi2fanxing/blob/master/src/fans.tb.sync/main.go 消费端代码
由golang从kafka拉数据统计 , 并把结果写入到 dwa_fx_fans_dau_cnt
结果存放到统计结果数据库 dwa_fx_fans_dau_cnt


# webmonitor
http://gitlab.fxwork.cn/analyze/webmonitor/tree/master/analyze/src/webmonitor

git@192.168.0.143:analyze/fxwebloadtime.git

#  内嵌页主播吸引力统计
http://gitlab.fxwork.cn/analyze/anchor-attraction/tree/master/src

# 
http://gitlab.fxwork.cn/analyze/jsontransfer/tree/master/src/jsonlog
fx.consumeclientfrom  fx_mobilekg_consume
fx_mobilekg_recharge fx.rechargeclientfrom
