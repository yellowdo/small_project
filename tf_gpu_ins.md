# Ubuntu 16.04 Tensorflow GPU Install

#### Miniconda Download

- https://conda.io/miniconda.html

- [Python 3.6 64bit](https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh)

- Install

```
chmod 777 Miniconda3-latest-Linux-x86_64.sh 
./Miniconda3-latest-Linux-x86_64.sh
```

#### Tensorflow GPU 버전 설치

- Conda update

```
conda update conda
pip install --upgrade pip
```

- python 3.6

```
conda create --name tf_gpu python=3.6
source activate tf_gpu
```

- pip install

```
pip install tensorflow-gpu
pip install numpy scipy matplotlib scikit-learn jupyter
pip install keras opencv-python
```
