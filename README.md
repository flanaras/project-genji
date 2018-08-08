# project-genji

A repository with instructions to install Machine learning frameworks such as Caffe and Tensorflow with their corresponding dependencies. These instructions are mainly aimed for offline installations/computers.

# Version

Versions building for:

* Caffe 1.0 (master commit 379a3ba2d5421a6ac05afa4239c30739cc79f7b0) 
* TensorFlow r1.5 (git branch r1.5) 

The version of Caffe that was used can be found at [my fork of caffe that has been severely edited](https://github.com/flanaras/caffe/tree/dtt).

## Explainations

Wherever it states `@Online` means this is to be executed on a computer with internet access.
`@Genji` means execute on the offline computer (computer that the setup is for).

* note-1: Since I'm a fun of fish shell, I include that as well. 

* note-2: The computer I was setting up did not provide `tree` which I use, that's why that is included in 

* note-3: The build process on TF for an offline computer is tricky, yet not impossible.
I have corvered this process on [a previous post (flanaras.wordpress.com)](https://flanaras.wordpress.com/2018/03/16/build-tensorflow-on-an-offline-computer/).


## Files

* [installation.md](installation.md) is the main howto, showing which packages are required to build Caffe and TF.

* [tf-model.md](tf-model.md) explains how to download and train TF with an available model on cifar10, for offline computers.

* [inst-dbg.md](inst-dbg.md) shows how to build from sources the dgb with dgbserver and its dependencies. Dependencies other than those included in the [installation.md](installation.md).

* [stap.md](stap.md) contains the info gathered from my attempt trying to use it. It does **not** work with openSUSE tumbleweed since tumbleweed uses the latest kernel and stap does not support them.
