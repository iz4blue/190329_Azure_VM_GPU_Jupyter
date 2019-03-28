# Azure 계정 생성

1. [상세설명](https://github.com/MijeongJeon/181215_AIBootCamp_Azure_ML_StudioHOL)

# docker CE 설치

- https://docs.docker.com/install/linux/docker-ce/ubuntu/
- 단 이후 nvidia docker 와의 버전 호환성 때문에 최신 버젼에서 조금 낮은 버젼으로 설치 함


```bash
$ sudo apt-get update
$ sudo apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
$ sudo apt-get install -y docker-ce=5:18.09.3~3-0~ubuntu-bionic  containerd.io docker-ce-cli
```


# cuda 드라이버 설치

- https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=debnetwork

```bash
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
$ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda
```

# cuda 드라이버 로딩

```bash
$ sudo reboot
```

# nvidia docker 설치

- https://github.com/NVIDIA/nvidia-docker

```bash
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update

$ sudo apt-get install -y nvidia-docker2
$ sudo systemctl stop docker
$ sudo systemctl start docker
```


# docker container 저장소 변경하기

- https://success.docker.com/article/how-do-i-set-the-docker-daemon-options

```bash
$ sudo systemctl stop docker
$ sudo mkdir -p /opt/docker_container/
$ ps aux | grep docker
```

cat /etc/systemd/system/multi-user.target.wants/docker.service
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -g /opt/docker_container/

```bash
$ sudo mount /dev/sdb1 /opt/docker_container/
$ sudo systemctl daemon-reload
$ sudo systemctl start docker
```


# keras 용 docker 생성

```bash
$ git clone git@github.com:iz4blue/190329_Azure_VM_GPU_Jupyter.git
$ mkdir ~/Data
$ cd 190329_Azure_VM_GPU_Jupyter/keras
$ sudo make GPU=0
```
