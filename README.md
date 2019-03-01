# nvidia-archives

lazy to always wget then mv to rename tokens ! creating this !!

See releases :

https://github.com/wonderingabout/nvidia-archives/releases

![screenshot](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/cudnn%20git%20download.png?raw=true)

"it just works", as nvidia said !

cudnn 7.0.5 (recommended for tensorrt 3.0.4) or 7.1.4 for cuda 9.0 (deb) for ubuntu 16.04
tensorrt 3.0.4 for cuda 9.0 (deb) for ubuntu 16.04 

# Easy installs

## easy install help for cuda 9.0 ubuntu 16.04 (deb + apt-get):

on a brand new ubuntu 16.04, do not install anything, do **NOT** install nvidia-384, first run `sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo reboot` , then just !!

```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub && sudo apt-get update && sudo apt-get -y install cuda && sudo reboot
```

after reboot, check nvcc --version : 

```
nvcc --version
```

## easy install help for cuda 10.0 local deb for ubuntu 18.04 :

on a brand new ubuntu 18.04, do not install anything, do **NOT** install nvidia-410, first run `sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo reboot` , then just !!

```
wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64 && \
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb && \
sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub && \
sudo apt-get update && \
sudo apt-get -y install cuda && \
sudo reboot
```

after reboot, check nvcc --version : 

```
nvcc --version
```

## easy post-install for cuda 10.0 and before cudnn deb ubuntu 18.04 :

```
sudo nano ~/.bashrc && source ~/.bashrc
```

need to add this (at the end of the file, save and exit) 

```
# add paths for cuda-10.0
export PATH=${PATH}:/usr/local/cuda-10.0/bin

# tensorrt cuda and cudnn other paths needed
export CUDA_INSTALL_DIR=/usr/local/cuda
export CUDNN_INSTALL_DIR=/usr/local/cuda
```

![bashrc](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nano-bashrc.png?raw=true)

`nvcc --version` should just works : 

![nvcc-version-just-works](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nvcc-version-just-works.png?raw=true)

## easy install help for cudnn 7.0.5 ubuntu 16.04 (deb) for tensorrt 3.0.4 (tar) :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.0.5/libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.0.5/libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.0.5/libcudnn7-doc_7.0.5.15-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb libcudnn7-doc_7.0.5.15-1+cuda9.0_amd64.deb && sudo apt-get -y upgrade && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN
```
no need to reboot after that

## easy install help for cudnn 7.4.x (latest) for cuda 10.0 ubuntu 18.04 (deb) :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.4.x-cuda10/libcudnn7_7.4.2.24-1+cuda10.0_amd64.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.4.x-cuda10/libcudnn7-dev_7.4.2.24-1+cuda10.0_amd64.deb https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.4.x-cuda10/libcudnn7-doc_7.4.2.24-1+cuda10.0_amd64.deb && sudo dpkg -i libcudnn7_7.4.2.24-1+cuda10.0_amd64.deb libcudnn7-dev_7.4.2.24-1+cuda10.0_amd64.deb libcudnn7-doc_7.4.2.24-1+cuda10.0_amd64.deb && sudo apt-get -y upgrade && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN
```
do not reboot yet, but do the post-install (needed) of adding paths

# else, alternative cudnn 7.1.x deb for cuda 9.0 to install later tensorrt 4.0.x tar :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt4.0.x-cudnn7.1.x/libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt4.0.x-cudnn7.1.x/libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt4.0.x-cudnn7.1.x/libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && sudo apt-get -y upgrade && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN
```

## easy post-install 2 after cudnn :
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

reboot is still not needed

## Easy install for tensorrt 3.0.4 ubuntu 16.04 (deb) :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt3.0.4/nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo apt-get update && sudo apt-get -y install tensorrt && sudo apt-get -y install python-libnvinfer-doc && sudo apt-get -y install uff-converter-tf && sudo apt-get install -y swig && dpkg -l | grep TensorRT && sudo reboot
```
A reboot is appreciated to finalize the install of tensorrt


## (alternative way) Easy install of tensorrt 3.0.4 + pycuda (tar)

tar install allows to install pycuda (`.whl` and `.so`)

all these instructions are [thanks to, adapted for 3.0.4](https://kezunlin.me/post/dacc4196/)

post install first : 

```
sudo nano ~/.bashrc && source ~/.bashrc
```

add these lines (includes tensorrt and the later needed cuda+cudnn install dir other paths needed to export) : 

```
# tensorrt tar install path
export LD_LIBRARY_PATH=/opt/tensorrt/lib:$LD_LIBRARY_PATH

# tensorrt cuda and cudnn other paths needed
export CUDA_INSTALL_DIR=/usr/local/cuda
export CUDNN_INSTALL_DIR=/usr/local/cuda
```

then the tar install :

```
cd ~ && wget https://github.com/wonderingabout/nvidia-archives/releases/download/run-tar-install/TensorRT-3.0.4.Ubuntu-16.04.3.x86_64.cuda-9.0.cudnn7.0.tar.gz && tar zxvf TensorRT-3.0.4.Ubuntu-16.04.3.x86_64.cuda-9.0.cudnn7.0.tar.gz && ls TensorRT-3.0.4 && sudo mv TensorRT-3.0.4 /opt/ && cd /opt && ls && sudo ln -s TensorRT-3.0.4/ tensorrt && sudo apt-get -y install python-pip && pip --version
```

then add cuda.h file in /etc/profile.d as explained here (pycuda is faulty, not us), install pycuda separately : http://0561blue.tistory.com/m/13?category=627413

```
sudo nano /etc/profile.d/cuda.h
```

add this line : 

```
export PATH=/usr/local/cuda-9.0/bin:$PATH
```

then save and exit, then :

notes 2019 : do the same with a cuda.sh file now
notes 2019 : and **reboot** !!! rebooting fixed pycuda install !!

```
sudo nano /etc/profile.d/cuda.sh
```
then save and exit, then :

```
sudo su -
pip install pycuda

```

sucess !!

![pycuda-sucess](https://github.com/wonderingabout/nvidia-archives/blob/cuda9.0/pictures/pycuda%20sucess.png?raw=true)

then either in root mode or not, do :

```
cd /opt/tensorrt/python && sudo pip2 install tensorrt-3.0.4-cp27-cp27mu-linux_x86_64.whl
cd /opt/tensorrt/uff && sudo pip2 install uff-0.2.0-py2.py3-none-any.whl
which convert-to-uff
sudo apt-get -y install tree && cd /opt/tensorrt && tree include/ && cd lib && ls && cd .. && tree bin && cd samples/sampleMNIST && ls && make -j8 && cd /opt/tensorrt/bin && ./sample_mnist
```

example of pycuda works : 

![pycuda-works](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/pycuda%20works.png?raw=true)

example of result : 

![tensorrt-compile](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/tensorrt%20tar%204.png?raw=true)

You can now reboot if you want, to finalize

Then during the bazel install, tensorrt path needs to be this instead : 

`/opt/tensorrt/lib/`


## (outdated, needs to add pycuda install steps too) Easy install of tensorrt 4.0.x + pycuda (tar)

tar install allows to install pycuda (`.whl` and `.so`)

all these instructions are [thanks to, adapted for 3.0.4](https://kezunlin.me/post/dacc4196/)

post install first : 

```
sudo nano ~/.bashrc && source ~/.bashrc
```

add these lines if not already added (includes tensorrt and the later needed cuda+cudnn install dir other paths needed to export) : 

```
# tensorrt tar install path
export LD_LIBRARY_PATH=/opt/tensorrt/lib:$LD_LIBRARY_PATH

# tensorrt cuda and cudnn other paths needed
export CUDA_INSTALL_DIR=/usr/local/cuda
export CUDNN_INSTALL_DIR=/usr/local/cuda
```

then the tar install :

```
cd ~ && wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt4.0.x-cudnn7.1.x/TensorRT-4.0.1.6.Ubuntu-16.04.4.x86_64-gnu.cuda-9.0.cudnn7.1.tar.gz && tar zxvf TensorRT-4.0.1.6.Ubuntu-16.04.4.x86_64-gnu.cuda-9.0.cudnn7.1.tar.gz && ls TensorRT-4.0.1.6 && sudo mv TensorRT-4.0.1.6 /opt/ && cd /opt && ls && sudo ln -s TensorRT-4.0.1.6/ tensorrt && cd /opt/tensorrt/python && sudo apt-get -y install python-pip && pip --version && sudo pip2 install tensorrt-4.0.1.6-cp27-cp27mu-linux_x86_64.whl && cd /opt/tensorrt/uff && sudo pip2 install uff-0.4.0-py2.py3-none-any.whl && which convert-to-uff && cd ../graphsurgeon && sudo pip2 install graphsurgeon-0.2.0-py2.py3-none-any.whl && sudo apt-get -y install tree && cd /opt/tensorrt && tree include/ && cd lib && ls && cd .. && tree bin && cd samples/sampleMNIST && ls && make -j8 && cd /opt/tensorrt/bin && ls && cp sample_mnist ../lib && cd ../lib && ./sample_mnist
```

# Alternative ways

## optionnal (can be skipped) post install of cuda : 

```
sudo nano /etc/environment
```

not needed, but if you want : add this (including the `:` ,at the the end of file, before `"`, save and exit):
`:/usr/local/cuda-9.0/bin`

![etc-environment](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nano-etc-environment.png?raw=true)

```
sudo reboot
```


# Ultimate install (deb), all in one (for splurgist people) cuda9.0+cudnn7.1.4+paths+reboot1+tensorrt3.0.4+reboot2 :

```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub && sudo apt-get update && sudo apt-get -y install cuda && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN && sudo nano /etc/environment && sudo nano ~/.bashrc && source ~/.bashrc && sudo reboot
# after reboot, do
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt3.0.4/nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo apt-get update && sudo apt-get -y install tensorrt && sudo apt-get -y install python-libnvinfer-doc && sudo apt-get -y install uff-converter-tf && sudo apt-get install -y swig && dpkg -l | grep TensorRT && sudo reboot
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
