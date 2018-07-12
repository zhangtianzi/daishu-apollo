### Configuration of IPC
- Nuvo-5095GC
- GPU:GTX-1050Ti
- CPU:i7-6700@3.4GHZ×8
- Memory: 32GB
### System Install
Apollo officially recommended to use ubuntu14.04
- [Install ubuntu 14.04.3](https://github.com/ApolloAuto/apollo/blob/r2.5.0/docs/howto/how_to_install_ubuntu.md)
- Update and Upgrade
    ```
    sudo apt-get update; sudo apt-get upgrade
    ```
- Install the Linux 4.4 kernel:
    ```
    sudo apt-get install linux-generic-lts-xenial
    ```
- Reboot your system using the reboot command
    ```
    sudo reboot
    ```
### Installing the Apollo Kernel
Apollo-kernel is a real-time kernel,if you want to run your apollo2.5 in a real car,please install it.
- Downloaded the release package and install it: [linux-4.4.32-apollo-1.5.0.tar.gz](https://github.com/ApolloAuto/apollo-kernel/releases)
    ```
    tar zxvf linux-4.4.32-apollo-1.5.0.tar.gz
    cd install
    sudo bash install_kernel.sh
    ```
- Reboot your system 

- [Optional] If you are using CAN card for interface,build the CAN driver source code according to the vendor's instructions

### [Optional] Install NVIDIA GPU Driver
The Apollo runtime in the vehicle requires the NVIDIA GPU Driver. You must install the NVIDIA GPU driver with specific options.If you have a NVIDIA GPU, please install the Driver  following the steps below 

- Download the installation files
    ```
    wget http://us.download.nvidia.com/XFree86/Linux-x86_64/375.39/NVIDIA-Linux-x86_64-375.39.run
    ```
- Start the driver installation

    ```
    chmod +x ./NVIDIA-Linux-x86_64-375.39.run
    sudo bash ./NVIDIA-Linux-x86_64-375.39.run --no-opengl-files --no-x-check --no-kernel-module
    ```
- Reboot your system

### Install Docker and Apollo
- Download apollo
    ```
    git clone https://github.com/ApolloAuto/apollo.git
    ```
- Installing Docker Environment
    ```
    cd apollo/
    bash ./docker/setup_host/install_docker.sh
    ```
- Pull the apollo-docker image
    ```
    bash ./docker/scripts/dev_start.sh -C
    ```
- checkout to apollo-2.5.0
    ```
    git checkout origin/r2.5.0
    ```
- Enter apollo docker environment
    ```
    bash ./docker/scripts/dev_into.sh
    ```
- Build apollo
    ```
    bash apollo.sh build
    ```
- Start apollo
    ```
    bash scripts/bootstrap.sh
    ```
- Use your host machine browser to access Dreamview web service in with URL http://localhost:8888.
