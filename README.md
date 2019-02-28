# nvidia-archives

lazy to always wget then mv to rename tokens ! making this !!

current master version : 

```
ubuntu 18.04
CUDA 10.0 deb
cudnn 7.5.0 deb for cuda 10.0
tensorRT 5.0.2 deb for cuda 10.0
```

See releases :

https://github.com/wonderingabout/nvidia-archives/releases

![screenshot](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/cudnn%20git%20download.png?raw=true)

"it just works", as nvidia said !

# Easy installs

## easy install help for cuda 10.0 local deb for ubuntu 18.04 :

- if you are on ubuntu server, you dont have X server issues, so you 
can start directly at 2)

- but if like most people you are on ubuntu desktop, on a brand new 
ubuntu **desktop** 18.04, it is easier to do the install in 2 steps : 

### 0) upgrade system

```sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo reboot```

### 1) install display driver only from ppa

this may seem uneeded, but installing the cuda 10.0 directly in 
desktop ubuntu when nouveau is the default display driver often 
breaks the X server

but the ppa version has been tested to work
for cuda 10.0, install nvidia-driver-410 metapackage

```sudo apt-get -y install nvidia-driver-410 && sudo reboot```

### 2) install cuda 10.0 deb local ubuntu 18.04 :

```
# install some cuda dependencies && \
sudo apt-get install gcc dkms build-essential && \
# download and install cuda && \
wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 && \
ls && \
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 && \
sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub && \
sudo apt-get update && \
sudo apt-get -y install cuda
```

do not reboot yet, do the post-install first : 

## easy post-install for cuda 10.0 and before cudnn deb ubuntu 18.04 :

```
sudo nano ~/.bashrc && source ~/.bashrc
```

need to add this (at the end of the file, save and exit) 

```
# add paths for cuda-10.0
export PATH=${PATH}:/usr/local/cuda-10.0/bin

# other nvidia paths that can be useful, for example for tensorrt
export CUDA_INSTALL_DIR=/usr/local/cuda
export CUDNN_INSTALL_DIR=/usr/local/cuda
```

![bashrc](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nano-bashrc.png?raw=true)

`nvcc --version` should just works : 

![nvcc-version-just-works](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nvcc-version-just-works.png?raw=true)

now you can reboot to finalize

```sudo reboot```

## easy install help for cudnn 7.5.0 deb for cuda 10.0 deb ubuntu 18.04 :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.5.0deb-cuda10.0deb/libcudnn7_7.5.0.56-1+cuda10.0_amd64.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.5.0deb-cuda10.0deb/libcudnn7-dev_7.5.0.56-1+cuda10.0_amd64.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.5.0deb-cuda10.0deb/libcudnn7-doc_7.5.0.56-1+cuda10.0_amd64.deb && \
sudo dpkg -i libcudnn7_7.5.0.56-1+cuda10.0_amd64.deb libcudnn7-dev_7.5.0.56-1+cuda10.0_amd64.deb libcudnn7-doc_7.5.0.56-1+cuda10.0_amd64.deb && \
sudo apt-get -y upgrade && \
cp -r /usr/src/cudnn_samples_v7/ ~ && \
cd ~/cudnn_samples_v7/mnistCUDNN && \
make clean && make && \
./mnistCUDNN
```

## easy post-install after cudnn :

it is also advised to update database (reboot to finalize) :

```
locate libcudart.so && locate libcudnn.so.7 && pwd
```

then :

```
sudo updatedb && locate libcudart.so && locate libcudnn.so.7
```

should display something like this :

```
/usr/local/cuda-9.0/doc/man/man7/libcudart.so.7
/usr/local/cuda-9.0/targets/x86_64-linux/lib/libcudart.so
/usr/local/cuda-9.0/targets/x86_64-linux/lib/libcudart.so.9.0
/usr/local/cuda-9.0/targets/x86_64-linux/lib/libcudart.so.9.0.176
/usr/lib/x86_64-linux-gnu/libcudnn.so.7
/usr/lib/x86_64-linux-gnu/libcudnn.so.7.1.4
```

## Easy install for tensorrt 5.0.2 deb ubuntu 18.04 :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt5.0.2deb-cuda10.0-ubuntu1804/nv-tensorrt-repo-ubuntu1804-cuda10.0-trt5.0.2.6-ga-20181009_1-1_amd64.deb && \
sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && \
sudo apt-get update && \
sudo apt-get -y install tensorrt && \
sudo apt-get -y install python-libnvinfer-doc && \
sudo apt-get -y install uff-converter-tf && \
sudo apt-get install -y swig && \
dpkg -l | grep TensorRT
```
A reboot can be appreciated to finalize the install of tensorrt

# Ultimate install (deb), all in one (for splurgist people) :

(unfinished)

```
# cuda 10.0 deb : 
# cudnn 7.5.0 deb :
# tensorrt 5.0.2 deb :

```

add paths as we saw earlier then reboots are included

# Credits : 

Biggest sources : 

- https://medium.com/@mishra.thedeepak/cuda-and-cudnn-installation-for-tensorflow-gpu-79beebb356d2

- https://kezunlin.me/post/dacc4196/

Smaller sources :

- https://docs.nvidia.com/deeplearning/sdk/tensorrt-archived/tensorrt_304/tensorrt-install-guide/index.html

- https://developer.nvidia.com/rdp/cudnn-archive

- https://developer.nvidia.com/nvidia-tensorrt3-download

- https://medium.com/@zhanwenchen/install-cuda-and-cudnn-for-tensorflow-gpu-on-ubuntu-79306e4ac04e
