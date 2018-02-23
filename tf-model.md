# TF Model:

## Cifar10

### Download and store data
```
wget https://www.cs.toronto.edu/~kriz/cifar-10-binary.tar.gz
mkdir /tmp/cifar10_data
cp cifar-10-binary.tar.gz /tmp/cifar10_data
tar xzf cifar-10-binary.tar.gz
```

### Download model
```
wget https://github.com/tensorflow/models/archive/r1.5.zip
unzip r1.5.zip
```

### Train
```
python tutorials/image/cifar10/cifar10_train.py
python tutorials/image/cifar10/cifar10_multi_gpu_train.py
```
