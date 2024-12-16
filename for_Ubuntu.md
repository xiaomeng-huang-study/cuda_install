# How to install CUDA / cuDNN on Ubuntu

## Install NVIDIA drivers

### Update & upgrade
```shell
sudo apt update
```

### Remove previous NVIDIA installation
```shell
sudo apt autoremove nvidia* --purge
```

### Check Ubuntu devices
```shell
ubuntu-drivers devices
```
You will install the NVIDIA driver whose version is tagged with __recommended__


### Install Ubuntu drivers
```shell
sudo ubuntu-drivers autoinstall
```

### Install NVIDIA drivers
(For example: version is 550)

```shell
sudo apt install nvidia-driver-550
```

### Reboot & Check
```shell
reboot
```
after restart verify that the following command works
```shell
nvidia-smi
```

## Install CUDA drivers

### Update & upgrade
```shell
sudo apt update && sudo apt upgrade
```

### Install CUDA toolkit
```shell
sudo apt install nvidia-cuda-toolkit
```

### Check CUDA install
```shell
nvcc --version
```

## Install cuDNN

### Download cuDNN .deb file
You can download cuDNN file [here](https://developer.nvidia.com/cudnn-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local). 
Select the cuDNN version for the appropriate CUDA version, which is the version that appears when you run:
```shell
nvcc --version
```

## Test CUDA on Pytorch


### Create a virtualenv and activate it

### Install pytorch
```shell
pip3 install torch torchvision torchaudio
```

### Open Python and execute a test
```python
import torch
print(torch.cuda.is_available()) # should be True

t = torch.rand(10, 10).cuda()
print(t.device) # should be CUDA
```

## Configuration for CUDA_HOME
use 
```shell
which nvcc
```
to get the location of cuda and nvcc
Normally: 
cuda: /usr/local/cuda
nvcc: /usr/local/cuda/bin/nvcc
(Adapt the 1. line in the following code)
```shell
export CUDA_HOME=/usr/local/cuda 
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH
```
