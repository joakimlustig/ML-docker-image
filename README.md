# ML Docker Image

## Description
This repo contains a docker image with everything that is required to run som popular ML frameworks on the GPU, such as sklearn, Tensorflow and Keras. It also contains a setup with Jupyter notebooks, that will open in your browser. It also mounts whichever folder you are in when you launch the docker container.

## Requirements
- docker installed on host
- nvidia-docker installed on host
- Nvidia GPU on host
- CUDA driver installed on host

## How to install Docker and CUDA driver on host

### Install docker
```
curl -O http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
dpkg -i ./cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
apt-get update
apt-get install cuda -y
```
### Verify that CUDA was installed correctly
```
nvidia-smi # Should display GPU details
```
### Install nvidia-docker
```
wget https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
sudo dpkg -i nvidia-docker*.deb
```
### Verify that nvidia-docker can access GPU
```
sudo nvidia-docker run --rm nvidia/cuda nvidia-smi # Should display the same as nvidia-smi except the processes
```
### Launch the docker image

### Build the image
```
docker build -t docker build -t ml-container .
```
### Launch the container
```
cd /path/to/project/folder # go to your project folder
sudo nvidia-docker run -v `pwd`/:/workspace/ --rm --name tf1 -p 8888:8888 -p 6006:6006 ml:latest jupyter notebook --allow-root
```