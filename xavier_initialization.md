# Initial Configurations for Jetson Xavier AGX
* Jetson Xavier AGX 초기 설정방법 정리
* 따라하다 실패해도 책임 안짐



## 1. Software Installation
### 1.1. Jetpack
* Jetpack 4.4.1 (17 Nov. 2020)
    * Jetpack SDK Download: https://developer.nvidia.com/embedded/jetpack, Login Required.
    * Communication devices (such as Wi-Fi Card) should be removed. The devices possibly interfere post-installation process.
    * Set Flashing mode: 1) Press Recovery button, 2) Press Power button, 3) Release them, 4) Check an Nvidia USB connection by "lsusb" command
    * Reboot the AGX when the ssh connection window is appeared in an host PC.
    * Finalize basic installations for the AGX.
    * Start post-installation process via SSH connection.

### 1.2. APT packages
* Nano Editor: sudo apt update && sudo apt install -y nano

### 1.3. Performance Monitoring
* jtop: https://github.com/rbonghi/jetson_stats
    * sudo apt update && sudo apt install -y python-pip python3-pip && sudo -H pip install -U jetson-stats
    * Reboot or sudo systemctl restart jetson_stats.service
    * sudo jtop

### 1.4. Communication Setup
* Wi-Fi
    * Some M.2 Key E devices are available withoiut kernal compile process.
    *

* VPN Client for fixed IP
    * sudo apt update && sudo apt install -y openvpn easy-rsa 
    * ls -al /usr/sbin/openvpn ==> Check existance of the binary file
    * Assume that __"your VPN client path"__==> __PPP__ and __"your VPN service name"__ ==> __SSS__
    * mkdir -p __PPP__
    * echo -e "[Unit]\nDescription=VPN Client\n[Service]\nType=simple\nUser=root\nExecStart=/usr/sbin/openvpn __PPP__/client.conf\nWorkingDirectory=__PPP__\nRestart=always\n[Install]\nWantedBy=multi-user.target" | sudo tee -a /etc/systemd/system/__SSS__.service > /dev/null
    * sudo systemctl daemon-reload 
    * sudo systemctl enable __SSS__
    * sudo systemctl start __SSS__
    * sudo systemctl status __SSS__



## 2. Mount External Storages
### 2.1. Disk Properties
* __Must__ set "ext4" partition if you want use docker images!
* Check disk name: sudo fdisk -l
* Check UUID and partition type: sudo blkid

### 2.2. Permanent Mount
* Make a directory for disk mount: mkdir -p __"mount path"__
* Add disk properties to /etc/fstab
* echo -e " UUID=__"your UUID"__ __"mount path"__ ext4 defaults 0 0" | sudo tee -a /etc/fstab > /dev/null



## 3. Modifications for Docker Environments
* sudo usermod -aG docker $USER, Reboot Required
* mkdir -p __"your docker path"__
* Add "data-root" option in "/lib/systemd/system/docker.service" file
    * ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --data-root=__"your docker path"__
    * In my case, sed -i '/ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock/ c ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --data-root=/home/nvidia/mount/containerd/' /lib/systemd/system/docker.service




## 4. 

