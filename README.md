# nvidia-archives

lazy to always wget then mv to rename tokens ! creating this !!

See releases :

https://github.com/wonderingabout/nvidia-archives/releases

![screenshot](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/cudnn%20git%20download.png?raw=true)

"it just works", as nvidia said !

cudnn 7.1.4 for cuda 9.0 (deb) for ubuntu 16.04
tensorrt 3.0.4 for cuda 9.0 (deb) for ubuntu 16.04 

# Easy installs

## easy install help for cuda 9.0 ubuntu 16.04 :

```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub && sudo apt-get update && sudo apt-get -y install cuda
```

do not reboot yet, but keep installing cudnn 7.1.4

## easy install help for cudnn 7.1.4 ubuntu 16.04 :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN
```
do not reboot yet, but do the post-install (needed) of adding paths

## easy post-install for cuda 9.0 cudnn 7.1.4 ubuntu 16.04 :

```
sudo nano /etc/environment && sudo nano ~/.bashrc && source ~/.bashrc && sudo reboot
```

in first file need to add this (including the `:` ,at the the end of file, before `"`, save and exit):
`:/usr/local/cuda-9.0/bin`

in second file need to add this (at the end of the file, save and exit)

```
# add paths for cuda-9.0
export PATH=${PATH}:/usr/local/cuda-9.0/bin
export CUDA_HOME=${CUDA_HOME}:/usr/local/cuda:/usr/local/cuda-9.0
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-9.0/lib64
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64
```
![etc-environment](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nano-etc-environment.png?raw=true)
![bashrc](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nano-bashrc.png?raw=true)

A reboot is included to finalize the install of cuda and cudnn

`nvcc --version` should just work now : 

![nvcc-version-just-works](https://github.com/wonderingabout/nvidia-archives/blob/master/pictures/nvcc-version-just-works.png?raw=true)

it is also advised to update database (reboot to finalize) :

```
locate libcudart.so && locate libcudnn.so.7 && pwd && sudo updatedb && locate libcudart.so && locate libcudnn.so.7
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

## easy install for tensorrt 3.0.4 ubuntu 16.04 :

```
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt3.0.4/nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo apt-get update && sudo apt-get -y install tensorrt && sudo apt-get -y install python-libnvinfer-doc && sudo apt-get -y install uff-converter-tf && sudo apt-get install -y swig && dpkg -l | grep TensorRT && sudo reboot
```
A reboot is included to finalize the install of tensorrt

# Ultimate install, all in one (for splurgist people) cuda9.0+cudnn7.1.4+paths+reboot1+tensorrt3.0.4+reboot2 :

```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb && sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub && sudo apt-get update && sudo apt-get -y install cuda && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && wget https://github.com/wonderingabout/nvidia-archives/releases/download/cudnn7.1.4/libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7-dev_7.1.4.18-1+cuda9.0_amd64.deb && sudo dpkg -i libcudnn7-doc_7.1.4.18-1+cuda9.0_amd64.deb && cp -r /usr/src/cudnn_samples_v7/ ~ && cd ~/cudnn_samples_v7/mnistCUDNN && make clean && make && ./mnistCUDNN && sudo nano /etc/environment && sudo nano ~/.bashrc && source ~/.bashrc && sudo reboot
# after reboot, do
wget https://github.com/wonderingabout/nvidia-archives/releases/download/tensorrt3.0.4/nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64.deb && sudo apt-get update && sudo apt-get -y install tensorrt && sudo apt-get -y install python-libnvinfer-doc && sudo apt-get -y install uff-converter-tf && sudo apt-get install -y swig && dpkg -l | grep TensorRT && sudo reboot
```

add paths as we saw earlier then reboots are included

# Credits : 

- https://medium.com/@mishra.thedeepak/cuda-and-cudnn-installation-for-tensorflow-gpu-79beebb356d2

- https://medium.com/@zhanwenchen/install-cuda-and-cudnn-for-tensorflow-gpu-on-ubuntu-79306e4ac04e

- https://developer.nvidia.com/rdp/cudnn-archive

- https://developer.nvidia.com/nvidia-tensorrt3-download
