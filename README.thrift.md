brew install thrift;

wget https://sourceforge.net/projects/boost/files/boost/1.61.0/boost_1_61_0.tar.gz/download -O /data1/softwares/tarball/boost_1_61_0.tar.gz;
tar xvzf /data1/software/tarball/boost_1_61_0.tar.gz -C /data1/software;
cd /data1/software/boost_1_61_0;
./bootstrap.sh —prefix=/usr/local/boost;
sudo ./b2 threading=multi address-model=64 variant=release stage install



#先到官网下载libevent包，并解压，然后进去该目录(目录路径：/usr/local)。

./configure —prefix=/usr/local  
make  
sudo make install

#brew install openssl
#然后再使用xcode-select -p命令查找xcode安装所在目录
#cd /Applications/Xcode.app/Contents/Developer && find . -name ssl.h
#cp -R /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/swift-migrator/sdk/MacOSX.sdk/usr/include/openssl /usr/local/include/

wget http://ftp.gnu.org/gnu/bison/bison-2.7.tar.gz -O /data1/software/tarball/bison-2.7.tar.gz;
tar xvzf /data1/software/tarball/bison-2.7.tar.gz -C /data1/software;
cd /data1/software/bison-2.7;
./configure --prefix=/usr/local/bison.2.7;
make;
make install;
mv /usr/bin/bison /usr/bin/bison.bk;
ln -s /usr/local/bison.2.7/bin/bison /usr/bin/bison;

wget http://ftp.gnu.org/gnu/libtool/libtool-2.4.tar.gz -O /data1/software/tarball/libtool-2.4.tar.gz;
tar xvzf /data1/software/tarball/libtool-2.4.tar.gz -C /data1/software/;
cd /data1/software/libtool-2.4;
./configure;
make;
make install;

wget http://mirrors.kernel.org/gnu/m4/m4-1.4.13.tar.gz -O /data1/software/tarball/m4-1.4.13.tar.gz \
         && tar -xzvf /data1/software/tarball/m4-1.4.13.tar.gz -C /data/software/ \
         && cd /data/software/m4-1.4.13 \
         && ./configure --prefix=/usr/local \
         && make && make install ;

wget http://mirrors.kernel.org/gnu/autoconf/autoconf-2.65.tar.gz -O /data1/software/tarball/autoconf-2.65.tar.gz \
         && tar -xzvf /data1/software/tarball/autoconf-2.65.tar.gz -C /data1/software/ \
         && cd /data/software/autoconf-2.65 \
         && ./configure --prefix=/usr/local \
         && make && make install ;


wget http://mirrors.kernel.org/gnu/automake/automake-1.15.tar.gz  -O /data1/software/tarball/automake-1.15.tar.gz \
         && tar -xzvf /data1/software/tarball/automake-1.15.tar.gz -C /data1/software/ \
         && cd /data1/software/automake-1.15 \
         && ./configure --prefix=/usr/local \
         && make && make install;

wget -c http://pkgconfig.freedesktop.org/releases/pkg-config-0.28.tar.gz -O /data1/software/tarball/pkg-config-0.28.tar.gz \
         && tar -xzvf /data1/software/tarball/pkg-config-0.28.tar.gz -C /data1/software/ \
         && cd /data1/software/pkg-config-0.28 \
         && ./configure  --prefix=/usr/local --with-internal-glib \
         && make && make install;

#http://www.77tek.com/?p=251

#wget -c https://www.apache.org/dist/thrift/0.9.3/thrift-0.9.3.tar.gz -O /data1/software/tarball/thrift-0.9.3.tar.gz;
wget -C https://codeload.github.com/apache/thrift/zip/0.9.3 -O /data1/software/tarball/thrift-0.9.3.tar.gz;
tar xvzf /data1/software/tarball/thrift-0.9.3.tar.gz -C /data1/software;
cd /data1/software/thrift-0.9.3/;
cp /usr/local/share/aclocal/pkg.m4 aclocal/;
export CXXFLAGS="-std=c++11"
./bootstrap.sh;
./configure --prefix=/usr/local/thrift-0.9.1 --with-boost=/usr/local/boost --with-libevent=/usr/local/libevent.2.0.22
make CXXFLAGS=-stdlib=libstdc++  --with-cc-opt="-Wno-deprecated-declarations"
make install;



#设置环境变量
#THRIFT_HOME=/usr/local/thrift-0.9.3
#PATH=$JAVA_HOME/bin:$PATH:$THRIFT_HOME/bin
#export JAVA_HOME CLASSPATH PATH THRIFT_HOME


