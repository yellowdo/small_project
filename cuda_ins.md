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

- GPU memory reset
 
 * PID 확인
 
 `nvidia-smi`
 
 ```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.130                Driver Version: 384.130                   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1080    Off  | 00000000:01:00.0  On |                  N/A |
| 35%   50C    P8    15W / 200W |   7868MiB /  8112MiB |      3%      Default |
+-------------------------------+----------------------+----------------------+
|   1  GeForce GTX 1080    Off  | 00000000:02:00.0 Off |                  N/A |
| 21%   48C    P8    15W / 200W |   7718MiB /  8114MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1163      G   /usr/lib/xorg/Xorg                            83MiB |
|    0      2285      G   compiz                                        87MiB |
|    0      2452      G   /opt/teamviewer/tv_bin/TeamViewer              7MiB |
|    0     22698      C   /home/do/miniconda3/envs/tf_gpu/bin/python  7685MiB |
|    1     22698      C   /home/do/miniconda3/envs/tf_gpu/bin/python  7707MiB |
+-----------------------------------------------------------------------------+
```

 * kill process (PID : 22698 kill)
 
 `sudo kill -9 22698`
 
 ```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.130                Driver Version: 384.130                   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1080    Off  | 00000000:01:00.0  On |                  N/A |
| 26%   48C    P8    15W / 200W |    185MiB /  8112MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   1  GeForce GTX 1080    Off  | 00000000:02:00.0 Off |                  N/A |
| 10%   48C    P8    15W / 200W |      2MiB /  8114MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1163      G   /usr/lib/xorg/Xorg                            85MiB |
|    0      2285      G   compiz                                        87MiB |
|    0      2452      G   /opt/teamviewer/tv_bin/TeamViewer             10MiB |
+-----------------------------------------------------------------------------+
```