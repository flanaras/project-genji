# Genji installation

## Machine Learning Requirements
Dependencies for both Caffe and TensorFlow

### General
#### Google Protobuf
https://github.com/google/protobuf
```
$ ./configure --prefix=$HOME/builds
$ make
$ make check
$ make install
$ #sudo ldconfig # refresh shared library cache.
```

#### OpenBLAS
https://github.com/xianyi/OpenBLAS
```
make
make install PREFIX=$HOME/builds
```

#### boost
http://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html
http://www.boost.org/users/history/version_1_66_0.html
```
$ ./bootstrap.sh --prefix=$HOME/builds
$ ./b2
$ ./b2 install
```

#### opencv
https://github.com/opencv/opencv
```
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=$HOME/builds ..
make
make install
tests...
```
##### test
https://github.com/opencv/opencv_extra
```
fish
set OPENCV_TEST_DATA_PATH ~/opencv_extra-3.4.0/testdata
<cmake_build_dir>/bin/opencv_test_core
```

#### gflags
https://github.com/gflags/gflags
```
mkdir build && cd build
export CXXFLAGS="-fPIC" && cmake -DCMAKE_INSTALL_PREFIX=$HOME/builds .. && make VERBOSE=1
make && make install
```

#### glog
https://github.com/google/glog
```
./configure --prefix=$HOME/builds
make
make install
```

#### hdf5
https://bitbucket.hdfgroup.org/projects/HDFFV/repos/hdf5/browse
https://support.hdfgroup.org/ftp/HDF5/current/src/
```
./configure --prefix=$HOME/builds  --enable-cxx
make
make check
make install
make check-install
```

#### leveldb
https://github.com/google/leveldb/archive/v1.20.tar.gz
https://gist.github.com/dustismo/6203329
```
make
scp out-static/lib* out-shared/lib* $HOME/builds/lib/
cd include/
scp -r leveldb $HOME/builds/include/
```

#### snappy
https://github.com/google/snappy
```
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=$HOME/builds
make
make install
```
### Cuda related
https://developer.nvidia.com/nccl/nccl-download
https://developer.nvidia.com/cudnn

### Python TF/C
https://www.python.org/downloads/release/python-2714/
```
wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
./configure --prefix=$HOME/builds/python2 --enable-optimizations --enable-unicode=ucs4 --enable-shared
make
make install
```
#### Add this version of python in the path before any others.
```
python --version
command -v python
python -m ensurepip --default-pip
```
#### Install wheel, numpy, six
```
#@Online
pip download -d `pwd`/pip-deps-install wheel numpy six
...
cd pydep-tf/
#@Genji
pip install *
...

#@Online
pip download -d `pwd`/pip-deps-tf-1.5.0 tensorflow-1.5.0-cp27-cp27mu-linux_x86_64.whl
```

### openmpi Dio-pro/TF
http://www.open-mpi.de/software/ompi/v3.0/
http://www.open-mpi.de/faq/?category=building
```
./configure --prefix=$HOME/builds
make
make install
```

## Build tools
### cmake
https://cmake.org/download/
```
./bootstrap --prefix=$HOME/builds
make
make install
```

### Bazel TF
https://github.com/bazelbuild/bazel/
```
https://github.com/bazelbuild/bazel/releases/download/0.10.1/bazel-0.10.1-without-jdk-installer-darwin-x86_64.sh
#wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.tar.gz
https://github.com/bazelbuild/bazel/releases/download/0.10.1/bazel-0.10.1-installer-linux-x86_64.sh
./bazel-0.10.1-installer-linux-x86_64.sh
```

## TensorFlow
### Acquire
https://www.tensorflow.org/install/install_sources
https://github.com/tensorflow/tensorflow

Configure TensorFlow:
```
#@Genji
git clone https://github.com/tensorflow/tensorflow.git
git checkout r1.5
./configure
> [...]
> CUDA: Y
> Set CUDA SDK version & path
> Set cuDNN version & path
> MPI: Y
> [...]
# Create the tmp folder for later use
bazel --output_user_root=`pwd`/../tf_tmp build --config=opt --fetch=false --config=cuda //tensorflow/tools/pip_package:build_pip_package
```
Transfer to online computer:
```
cd ..
tar zcf tf-configured.tar.gz tensorflow
```
prepare bazel for offline compilation
```
#@Online
scp $path/tf-configured.tar.gz .
tar zxf tf-configured.tar.gz
cd tensorflow
bazel --output_user_root=`pwd`/../tf_tmp fetch --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
./configure
# Configure as on Genji
bazel --output_user_root=`pwd`/../tf_tmp build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
cd ../tf_tmp/22b7191bf872641ec533c3a935b4af91/
# change hash to your own
tar zcf external.tar.gz external/
scp external.tar.gz $remote_host:$remote_path
```
back on the offline computer
```
#@Genji
cd $remote_path
tar zxf external.tar.gz
mv external $path_to_/tf_tmp/hash/
bazel --output_user_root=`pwd`/../tf_tmp build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
# win
```

## Caffe
https://github.com/BVLC/caffe
http://caffe.berkeleyvision.org/installation.html
```
cp Makefile.config.example Makefile.config
# Use cudnn
# opencv 3
# compute_* >=30
# blas := open
# python_include
# python_lib
# include_dirs
# library_dirs
# use nccl
make all
make test
make runtest
make pycaffe
```

## NVCaffe
### nasm
https://www.nasm.us/pub/nasm/releasebuilds/2.13.03/nasm-2.13.03.tar.gz
https://www.nasm.us/xdoc/2.13.03/html/nasmdocd.html#section-D.1
```
sh configure --prefix=$HOME/builds
make all
make install
```
### libjpeg turbo
# building info at BUILDING.md
https://sourceforge.net/projects/libjpeg-turbo/files/1.5.3/libjpeg-turbo-1.5.3.tar.gz/download
```
autoreconf -fiv
mkdir build
cd build
sh ../configure --prefix=$HOME/builds
make
make install
```
### NVCaffe build
```
use same conf file as Caffe + LIBRARY_NAME_SUFFIX := -nv # at the end of the file.
make same
```


## Personal
### perl for git
https://github.com/Perl/perl5/releases
```
./Configure -des -Dprefix=$HOME/builds
make
make test
make install
```

### git
https://github.com/git/git/
```
$ tar -zxf git-2.0.0.tar.gz
$ cd git-2.0.0
$ make configure
$ ./configure --prefix=$HOME/builds --with-perl=$HOME/builds/bin/perl
$ make all #doc info
$ make install #install-doc install-html install-info
```

### fish
https://github.com/fish-shell/fish-shell
```
# Get
FHISH_SHELL_VERSION=2.7.1
mkdir -p $HOME/local $HOME/fish_shell_tmp
cd $HOME/fish_shell_tmp
wget https://github.com/fish-shell/fish-shell/releases/download/${FHISH_SHELL_VERSION}/fish-${FHISH_SHELL_VERSION}.tar.gz

# build & install
tar xvzf fish-${FHISH_SHELL_VERSION}.tar.gz
cd fish-${FHISH_SHELL_VERSION}
./configure --prefix=$HOME/local --disable-shared
make
make install
```

### tree
