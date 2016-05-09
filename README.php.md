sudo kill -USR2 `cat /usr/local/php/var/run/php-fpm.pid`
sudo /usr/local/php/sbin/php-fpm
/usr/local/php/bin/php -i | less
/usr/local/php/bin/php -m
/usr/local/php/bin/phpize


sudo vi /usr/local/php/etc/php.ini
