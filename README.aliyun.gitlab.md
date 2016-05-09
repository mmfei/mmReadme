
wget -O /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6 https://www.fedoraproject.org/static/0608B895.txt
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
rpm -qa gpg*
#是否有显示下面的文字,是说明ok了
#gpg-pubkey-0608b895-4bd22942

rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

#下载puias repo
wget -O /etc/yum.repos.d/PUIAS_6_computational.repo https://gitlab.com/gitlab-org/gitlab-recipes/raw/master/install/centos/PUIAS_6_computational.repo

#安装gpgkey
wget -O /etc/pki/rpm-gpg/RPM-GPG-KEY-puias http://springdale.math.ias.edu/data/puias/6/x86_64/os/RPM-GPG-KEY-puias
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-puias

#验证epel 和 puias computational 是否显示了PUIAS_6_computational 和 epel
yum repolist

#安装依赖环境

yum -y update
yum -y groupinstall 'Development Tools'
yum -y install readline readline-devel ncurses-devel gdbm-devel glibc-devel tcl-devel openssl-devel curl-devel expat-devel db4-devel byacc sqlite-devel libyaml libyaml-devel libffi libffi-devel libxml2 libxml2-devel libxslt libxslt-devel libicu libicu-devel system-config-firewall-tui redis sudo wget crontabs logwatch logrotate perl-Time-HiRes git cmake libcom_err-devel.i686 libcom_err-devel.x86_64

#安装一下这个估计不用安装的
yum -y install python-docutils

#安装git
yum install zlib-devel perl-CPAN gettext curl-devel expat-devel gettext-devel openssl-devel
cd /data1/softwares/;
curl --progress https://www.kernel.org/pub/software/scm/git/git-2.1.3.tar.gz | tar xz;
cd git-2.1.3/;
./configure
make
make prefix=/usr/local/git-2.1.3 install

#编辑环境 , 让git默认使用新编译的
echo 'export PATH="/usr/local/git-2.1.3/bin:$PATH"' >> /etc/profile
source /etc/profile

#安装ruby
cd /data1/softwares/;
curl --progress ftp://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz | tar xz
cd ruby-2.1.2
./configure --disable-install-rdoc
make
make install


#检查环境
which ruby
ruby -v
gem -v

#改rubygem的源
gem source -r https://rubygems.org/
#gem source -a http://mirrors.aliyun.com/rubygems/
gem source -a http://ruby.taobao.org/
gem sources -l
gem install bundler --no-doc

######创建git系统用户账号
adduser --system --shell /bin/bash --comment 'GitLab' --create-home --home-dir /home/git/ git

#编辑sudoers file , 并搜索secure_path
#Defaults    secure_path = /sbin:/bin:/usr/sbin:/usr/bin
#改成
#Defaults    secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/usr/local/bin
visudo

#安装postgresql
rpm -Uvh http://yum.postgresql.org/9.3/redhat/rhel-6-x86_64/pgdg-centos93-9.3-1.noarch.rpm
yum install postgresql93-server postgresql93-devel

#创建软连接
ln -s /usr/pgsql-9.3/bin/pg_dump /usr/bin/pg_dump
ln -s /usr/pgsql-9.3/bin/pg_restore /usr/bin/pg_restore
ln -s /usr/pgsql-9.3/bin/psql /usr/bin/psql
#重命名启动脚本
mv /etc/init.d/{postgresql-9.3,postgresql}

#初始化数据库
service postgresql initdb
service postgresql start
chkconfig postgresql on

#配置数据库的账号和密码

su - postgres
export PATH=$PATH:/usr/pgsql-9.3/bin/
psql -d template1

psql (9.4.3)
template1=# CREATE USER git CREATEDB;
CREATE ROLE
template1=# CREATE DATABASE gitlabhq_production OWNER git;
CREATE DATABASE
template1=# \q
exit # exit uid=postgres, return to root


#whoami 确保自己是用root账号
whoami

#尝试用git账号登陆postgres
sudo -u git psql -d gitlabhq_production

#确定/var/lib/pgsql/9.3/data/pg_hba.conf里面
#旧:host    all             all             127.0.0.1/32            ident
#新:host    all             all             127.0.0.1/32            trust

#######################
#安装mysql
yum install -y mysql-server mysql-devel
chkconfig mysqld on
service mysqld start
#检测版本
mysql --version
#初始化
mysql_secure_installation
#创建git使用的数据库账号git , 密码为123456
mysql -u root -p < "CREATE USER 'git'@'localhost' IDENTIFIED BY '123456';CREATE DATABASE IF NOT EXISTS `gitlabhq_production` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;GRANT SELECT, LOCK TABLES, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER ON `gitlabhq_production`.* TO 'git'@'localhost';"

#尝试连接
sudo -u git -H mysql -u git -p -D gitlabhq_production





############Redis################
chkconfig redis on
cp /etc/redis.conf /etc/redis.conf.orig
#关闭redis的tcp监听
sed 's/^port .*/port 0/' /etc/redis.conf.orig | sudo tee /etc/redis.conf

#打开redis的socket监听
echo 'unixsocket /var/run/redis/redis.sock' | sudo tee -a /etc/redis.conf
echo -e 'unixsocketperm 0770' | sudo tee -a /etc/redis.conf

mkdir /var/run/redis
chown redis:redis /var/run/redis
chmod 755 /var/run/redis

if [ -d /etc/tmpfiles.d ]; then
    echo 'd  /var/run/redis  0755  redis  redis  10d  -' | sudo tee -a /etc/tmpfiles.d/redis.conf
fi
service redis restart
#把git账号加到redis组
usermod -aG redis git

###########GitLab#############

cd /home/git
sudo -u git -H git clone https://gitlab.com/gitlab-org/gitlab-ce.git -b 7-4-stable gitlab
cd /home/git/gitlab
sudo -u git -H cp config/gitlab.yml.example config/gitlab.yml
sudo -u git -H editor config/gitlab.yml
chown -R git log/
chown -R git tmp/
chmod -R u+rwX log/
chmod -R u+rwX tmp/
sudo -u git -H mkdir /home/git/gitlab-satellites
chmod u+rwx,g=rx,o-rwx /home/git/gitlab-satellites
chmod -R u+rwX tmp/pids/
chmod -R u+rwX tmp/sockets/
chmod -R u+rwX  public/uploads
sudo -u git -H cp config/unicorn.rb.example config/unicorn.rb
#查看是多少核的cpu
nproc
#编辑主机的cpu内核数量
sudo -u git -H editor config/unicorn.rb
sudo -u git -H cp config/initializers/rack_attack.rb.example config/initializers/rack_attack.rb
sudo -u git -H git config --global user.name "GitLab_mmfei"
sudo -u git -H git config --global user.email "wlfkongl@mmfei.com"
sudo -u git -H git config --global core.autocrlf input
sudo -u git -H cp config/resque.yml.example config/resque.yml
#编辑redis相关的信息
sudo -u git -H editor config/resque.yml



#配置gitlabdb
# PostgreSQL only:
# sudo -u git cp config/database.yml.postgresql config/database.yml

# MySQL only:
sudo -u git cp config/database.yml.mysql config/database.yml

# MySQL and remote PostgreSQL only:
# Update username/password in config/database.yml.
# You only need to adapt the production settings (first part).
# If you followed the database guide then please do as follows:
# Change 'secure password' with the value you have given to $password
# You can keep the double quotes around the password
# sudo -u git -H editor config/database.yml

# PostgreSQL and MySQL:
# Make config/database.yml readable to git only
sudo -u git -H chmod o-rwx config/database.yml




#############################
#Install Gems
#############################
cd /home/git/gitlab

# For PostgreSQL (note, the option says "without ... mysql")
#sudo -u git -H bundle config build.pg --with-pg-config=/usr/pgsql-9.3/bin/pg_config
#sudo -u git -H bundle install --deployment --without development test mysql aws

# Or for MySQL (note, the option says "without ... postgres")
sudo -u git -H bundle install --deployment --without development test postgres aws


############################
#Install gitlan shell
############################
# Run the installation task for gitlab-shell (replace `REDIS_URL` if needed):
sudo -u git -H bundle exec rake gitlab:shell:install[v2.1.0] REDIS_URL=unix:/var/run/redis/redis.sock RAILS_ENV=production

# By default, the gitlab-shell config is generated from your main GitLab config.
# You can review (and modify) the gitlab-shell config as follows:
sudo -u git -H editor /home/git/gitlab-shell/config.yml

# Ensure the correct SELinux contexts are set
# Read http://wiki.centos.org/HowTos/Network/SecuringSSH
restorecon -Rv /home/git/.ssh


