# nvidia-archives

lazy to always wget then mv to rename tokens ! making this !!

current master version : 

```
ubuntu 18.04
cuda 10.2
```

![cuda1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda1.png)

The steps below are provided for a fresh brand new ubuntu 18.04 :

"it just works", as nvidia said !

# Easy installs

## easy install help for cuda 10.2 local deb for ubuntu 18.04 :

### 0) upgrade system

```
sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo reboot
```

then : 

- if you are on ubuntu **server** (google cloud, etc..), you dont have X 
server issues, so you can continue directly at 
[2)](#2-install-cuda-102-deb-local-ubuntu-1804-)

- but if like most people you are on ubuntu desktop, on a brand new 
ubuntu **desktop** 18.04, it is easier to do the install in 2 steps: 

### 1) install display driver first

this may seem uneeded, but installing the cuda 10.2 directly in 
desktop ubuntu when nouveau is the default display driver often 
breaks the X server

It is possible to install the graphics driver from system 
official repositories or from a ppa.

More details about nvidia driver packages available for ubuntu here:
[here](https://packages.ubuntu.com/search?suite=default&section=all&arch=any&keywords=nvidia&searchon=names)

Also, for information about minimal nvidia driver version required 
to match a CUDA version, it can be found
[here](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html), 
for example we can see that the minimal nvidia graphics driver required 
to match cuda 10.2 is nvidia graphics driver version 440

Here we are using the example of a ppa install

```
sudo add-apt-repository -y ppa:graphics-drivers/ppa && \
sudo apt-get update && \
sudo apt-get -y install nvidia-driver-440 && \
sudo reboot
```

as you can see, it works after reboot : 

![ppa1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/ppa1.png)

we can also see the "software and updates" ubuntu 
menu display out of curiosity :

below, nvidia-driver-440 is displayed to be "open source", but 
dont mind it : we are using the proprietary driver as intended

![ppa2](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/ppa2.png)

### 2) install cuda 10.2 deb local ubuntu 18.04 :

```
# install some cuda dependencies && \
sudo apt-get install gcc dkms build-essential && \
# then follow instructions and command-line here: && \
# https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu && \
```

a few screenshots of the install process : 

![cuda1](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda1.png)
![cuda2](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda2.png)
![cuda3](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda3.png)

do not reboot yet, do the post-install first : 

## easy post-install for cuda 10.2 and before cudnn deb ubuntu 18.04 :

```
sudo nano ~/.bashrc
```

need to add this (at the end of the file, save and exit) 
as explained in 
[nvidia's official documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions)

```
# add paths for cuda-10.2
export PATH=/usr/local/cuda-10.2/bin:/usr/local/cuda-10.2/NsightCompute-2019.1${PATH:+:${PATH}}
```

same as in this screenshot : 

![cuda4](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda4.png)

then update system about the changes : 

```
source ~/.bashrc
```

now `nvcc --version` should just work (we also run `nvidia-smi` 
out of curiosity) : 

![cuda5](https://raw.githubusercontent.com/wonderingabout/nvidia-archives/master/pictures/10.0/cuda5.png)

now you can reboot to finalize

```
sudo reboot
```

## easy install help for cudnn latest version deb for cuda 10.2 deb ubuntu 18.04 :

**For cuDNN install, the trick is to remove all version names **
**in filenames and use generic commands instead !!**

```
cd ~ && \
wget https://github.com/wonderingabout/nvidia-archives/releases/download/cuda-10.2/libcudnn7.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cuda-10.2/libcudnn7-dev.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cuda-10.2/libcudnn7-doc.deb && \
sudo dpkg -i libcudnn7.deb libcudnn7-dev.deb libcudnn7-doc.deb && \
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

it is also advised to update database

first we check if the libs can be located

```
locate libcudart.so && locate libcudnn.so.7 && pwd
```

then, most likely you will not be able to locate them, so we 
update the database, then check again

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

A reboot can be appreciated to finalize the install of everything !

```
sudo reboot
```

and thats it !

it just works !!

# Credits : 

Biggest sources : 

- https://medium.com/@mishra.thedeepak/cuda-and-cudnn-installation-for-tensorflow-gpu-79beebb356d2

Smaller sources :

- https://developer.nvidia.com/rdp/cudnn-archive
- https://medium.com/@zhanwenchen/install-cuda-and-cudnn-for-tensorflow-gpu-on-ubuntu-79306e4ac04e
