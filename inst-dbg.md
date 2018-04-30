# Genji installation
Installing debug applications for easier debugging.


## DGB with dgbserver
https://blog.jetbrains.com/clion/2016/07/clion-2016-2-eap-remote-gdb-debug/
git://sourceware.org/git/binutils-gdb.git
```
git checkout -b gdb-7.11.1-release
./configure --target=x86_64-linux-gnu --with-python --prefix=$HOME/builds 
make
make install
./bin/x86_64-linux-gnu-gdb
./bin/x86_64-linux-gnu-gdbserver
cd ...
ln -s x86_64-linux-gnu-gdb gdb 
ln -s x86_64-linux-gnu-gdbserver gdbserver
```

### texinfo for gdb
http://ftp.gnu.org/gnu/texinfo/texinfo-6.5.tar.gz
```
./configure --prefix=$HOME/builds
make
make install
```
