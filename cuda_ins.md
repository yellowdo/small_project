# Ubuntu 16.04 CUDA 9.0 and cuDNN 7.1 Install

#### CUDA 9.0 Download

- [New Release](https://developer.nvidia.com/cuda-downloads)

- [9.0](https://developer.nvidia.com/cuda-90-download-archive)

 - Installation Instructions:

 ```
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```

- 버전 확인

`nvidia-smi`

#### cuDNN 7.1

- [New Release](https://developer.nvidia.com/rdp/cudnn-archive)

- [7.1.4](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.1.4/prod/9.0_20180516/cudnn-9.0-linux-x64-v7.1)

- include, lib64 파일 복사

```
cd cudnn-9.0-linux-x64-v7.1/
cd include/
sudo cp cudnn.h /usr/local/cuda/include
cd ..
cd lib64/
sudo cp libcu* /usr/local/cuda/lib64
```

- .bashrc 내용 추가

`gedit ~/.bashrc`

```
# add cuda tools to command path
export PATH=/usr/local/cuda/bin:${PATH}
export MANPATH=/usr/local/cuda/man:${MANPATH}

# add cuda libraries to library path
if [[ "${LD_LIBRARY_PATH}" != "" ]]
then
  export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH}
else
  export LD_LIBRARY_PATH=/usr/local/cuda/lib64
fi
```

- version 확인
`cat /usr/include/cudnn.h | grep -E "CUDNN_MAJOR|CUDNN_MINOR|CUDNN_PATCHLEVEL"`