# nvidia-archives

lazy to always wget then mv to rename tokens ! making this !!

current master version : 

```
ubuntu 18.04
CUDA 10.0 deb
cudnn 7.5.0 deb for cuda 10.0
tensorRT 5.0.2 deb for cuda 10.0
```

![cuda1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda1.png)

The steps below are provided for a fresh brand new ubuntu 18.04 :

"it just works", as nvidia said !

# Easy installs

## easy install help for cuda 10.0 local deb for ubuntu 18.04 :

- if you are on ubuntu server (google cloud, etc..), you dont have X 
server issues, so you can start directly at 
[2)](#2-install-cuda-100-deb-local-ubuntu-1804-)

- but if like most people you are on ubuntu desktop, on a brand new 
ubuntu **desktop** 18.04, it is easier to do the install in 2 steps : 

### 0) upgrade system

```
sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo reboot
```

### 1) install display driver only from ppa

this may seem uneeded, but installing the cuda 10.0 directly in 
desktop ubuntu when nouveau is the default display driver often 
breaks the X server

but the ppa version has been tested to work
for cuda 10.0, install nvidia-driver-410 metapackage

```
sudo add-apt-repository -y ppa:graphics-drivers/ppa && \
sudo apt-get update && \
sudo apt-get -y install nvidia-driver-410 && \
sudo reboot
```

as you can see, it works after reboot : 

![ppa1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/ppa1.png)

we can also see the "software and updates" ubuntu 
menu display out of curiosity : 

![ppa2](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/ppa2.png)

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

a few screenshots of the install process : 

![cuda1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda1.png)
![cuda2](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda2.png)
![cuda3](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda3.png)

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

same as in this screenshot : 

![cuda4](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda4.png)

now `nvcc --version` should just works (we also run `nvidia-smi` 
out of curiosity) : 

![cuda5](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda5.png)

now you can reboot to finalize

```
sudo reboot
```

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

some screenshots of the cudnn install process :

![cudnn1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cudnn1.png)
![cudnn2](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cudnn2.png)
![cudnn3](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cudnn3.png)
![cudnn4](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cudnn4.png)

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
/usr/local/cuda-10.0/doc/man/man7/libcudart.so.7
/usr/local/cuda-10.0/targets/x86_64-linux/lib/libcudart.so
/usr/local/cuda-10.0/targets/x86_64-linux/lib/libcudart.so.10.0
/usr/local/cuda-10.0/targets/x86_64-linux/lib/libcudart.so.10.0.130
/usr/lib/x86_64-linux-gnu/libcudnn.so.7
/usr/lib/x86_64-linux-gnu/libcudnn.so.7.5.0

```

## Easy install for tensorrt 5.0.2 deb ubuntu 18.04 :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt5.0.2deb-cuda10.0-ubuntu1804/nv-tensorrt-repo-ubuntu1804-cuda10.0-trt5.0.2.6-ga-20181009_1-1_amd64.deb && \
sudo dpkg -i sudo dpkg -i nv-tensorrt-repo-ubuntu1804-cuda10.0-trt5.0.2.6-ga-20181009_1-1_amd64.deb && \
sudo apt-key add /var/nv-tensorrt-repo-cuda10.0-trt5.0.2.6-ga-20181009/7fa2af80.pub && \
sudo apt-get update && \
sudo apt-get -y install tensorrt && \
# then if using python 2.7 like me : && \
sudo apt-get -y install python-libnvinfer-dev && \
# If you plan to use TensorRT with TensorFlow && \
# The graphsurgeon-tf package will also be installed with the above command : && \
sudo apt-get -y install uff-converter-tf && \
dpkg -l | grep TensorRT
```

source : [Nvidia TensorRT install guide PDF](https://developer.download.nvidia.com/compute/machine-learning/tensorrt/docs/5.0/GA_5.0.2.6/TensorRT-Installation-Guide.pdf)

A reboot can be appreciated to finalize the install of tensorrt

```
sudo reboot
```

and thats it !

it just works !!

# Credits : 

Biggest sources : 

- https://medium.com/@mishra.thedeepak/cuda-and-cudnn-installation-for-tensorflow-gpu-79beebb356d2

Smaller sources :

- https://developer.download.nvidia.com/compute/machine-learning/tensorrt/docs/5.0/GA_5.0.2.6/TensorRT-Installation-Guide.pdf

- https://developer.nvidia.com/rdp/cudnn-archive

- https://medium.com/@zhanwenchen/install-cuda-and-cudnn-for-tensorflow-gpu-on-ubuntu-79306e4ac04e
