# TF Model:

## Cifar10


### Download model
```
wget -O caffe-master.zip https://github.com/BVLC/caffe/archive/master.zip
unzip caffe-master.zip
```

### Download and store data
```
wget https://www.cs.toronto.edu/~kriz/cifar-10-binary.tar.gz
tar xzf cifar-10-binary.tar.gz
mv cifar-10-batches-bin/* caffe-master/data/cifar10/
```

### Create lmdb
```
cd caffe-master
./examples/cifar10/create_cifar10.sh
```

### Train
```
examples/cifar10/train_quick.sh
examples/cifar10/train_full.sh
```
