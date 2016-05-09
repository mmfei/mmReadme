sudo /usr/local/mysql/support-files/mysql.server start
sudo /usr/local/mysql/support-files/mysql.server restart

/usr/local/mysql/bin/mysql -u root -p

grant select,delete,insert,update on d_fanxing.* to fanxing_read@'10.1.0.%'  identified by 'kgeql@(!)read' ;
grant all privileges on *.*  to 'd_fanxing_root'@'10.1.0.%'  identified by 'kgeql@(!)tmp' ;

grant all privileges on dotproject_mmfei_com.*  to 'www'@'%'  identified by 'www.mmfei.com' ;
grant all privileges on dbName.*  to 'dbUser'@'ipList'  identified by 'password' ;

flush privileges;
