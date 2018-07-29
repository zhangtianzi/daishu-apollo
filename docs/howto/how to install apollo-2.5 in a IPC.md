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
***If you are using CAN card for interface,please click [here](http://note.youdao.com/noteshare?id=98235105a48a56fef98b2e8669975c3e&sub=494AE354217E43A6A8DA298497F326E0)***
- Downloaded the release package and install it: [linux-4.4.32-apollo-1.5.0.tar.gz](https://github.com/ApolloAuto/apollo-kernel/releases)
    ```
    tar zxvf linux-4.4.32-apollo-1.5.0.tar.gz
    cd install
    sudo bash install_kernel.sh
    ```
- Reboot your system 
### [Optional] Install NVIDIA GPU Driver
If you install apollo-kernel according to [this link](http://note.youdao.com/noteshare?id=98235105a48a56fef98b2e8669975c3e&sub=494AE354217E43A6A8DA298497F326E0)，maybe you've installed the Nvidia-Driver successfully.However,if you failed to do that ,don't worry,please follow the steps below:
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
- checkout to apollo-2.5.0
    ```
    git checkout origin/r2.5.0
    ```
- Pull the apollo-docker image
    ```
    bash ./docker/scripts/dev_start.sh -C
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
- Use your host machine browser to access Dreamview web service in with URL http://localhost:8888
