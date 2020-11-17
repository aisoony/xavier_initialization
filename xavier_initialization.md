# Initial Configurations for Jetson Xavier AGX


## 1. Software Installation
### 1.1. Jetpack
* Jetpack 4.4.1 (17 Nov. 2020)
    * Jetpack SDK Download: https://developer.nvidia.com/embedded/jetpack, Login Required.
    * Communication devices (such as Wi-Fi Card) should be removed. The devices possibly interfere post-installation process.
    * Reboot the AGX when the ssh connection window is appeared in an host PC.
    * Finalize basic installations for the AGX.
    * Start post-installation process via SSH connection.

### 1.2. APT packages
* Nano Editor: sudo apt update && sudo apt install -y nano

### 1.3. Performance Monitoring
* jtop: https://github.com/rbonghi/jetson_stats
    * sudo apt update && sudo -H pip install -U jetson-stats

### 1.4. Communication Setup
* Wi-Fi
    * Some M.2 Key E devices are available withoiut kernal compile process.
    *

* VPN Client for fixed IP
    * sudo apt update && sudo apt install -y openvpn easy-rsa libnfnetlink0 iptables iputils* libssl-dev liblzo2-dev libpam0g-dev netcat sshpass
    * ls -al /usr/sbin/openvpn ==> Check existance of the binary file
    * mkdir -p __"your VPN client path"__
    * echo -e "[Unit]\nDescription=VPN Client\n[Service]\nType=simple\nUser=root\nExecStart=/usr/sbin/openvpn __"your VPN client path"__/client.conf\nWorkingDirectory=__"your VPN client path"__\nRestart=always\n[Install]\nWantedBy=multi-user.target" | sudo tee -a /etc/systemd/system/__"your VPN service name"__.service > /dev/null
    * sudo systemctl daemon-reload 
    * sudo systemctl enable __"your VPN service name"__
    * sudo systemctl start __"your VPN service name"__
    * sudo systemctl status __"your VPN service name"__
    


## 2. Mount External Storages
### 2.1. Disk Configuration
### 2.2. 


## 3. Modifications for Docker Environments

## 4. 

