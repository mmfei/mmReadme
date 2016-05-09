卡在安装MySql-python上面了
cc -bundle -undefined dynamic_lookup -arch x86_64 -arch i386 -Wl,-F. build/temp.macosx-10.10-intel-2.7/_mysql.o -L/usr/local/mysql/lib/mysql -lmysqlclient -o build/lib.macosx-10.10-intel-2.7/_mysql.so
ld: library not found for -lmysqlclient
clang: error: linker command failed with exit code 1 (use -v to see invocation)
	error: command 'cc' failed with exit status 1

cd /data1/software/MySQL-python-1.2.3;
python setup.py build;


export LD_LIBRARY_PATH="/usr/local/mysql/lib:$LD_LIBRARY_PATH"
