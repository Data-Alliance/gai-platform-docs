# **Tier 2 Node Provider Setup Guide**

To all Tier 2 Node Providers: Please complete the Ubuntu OS setup according to the guide below before proceeding with the node installation. <br>
[Tier 2 Ubuntu OS Setting Guide](Ubuntu-OS-setup.md)
<br>

## **1. NVIDIA Graphics Driver Installation**

- After logging into Ubuntu, you must install the NVIDIA driver to ensure the system recognizes the GPU correctly.
- Remove Existing Drivers
    
    ```jsx
    $ sudo apt-get purge nvidia*
    $ sudo apt-get autoremove
    $ sudo apt-get autoclean
    
    $ sudo dpkg -l | grep nvidia
    $ sudo apt remove --purge {Package Name from the output}
    ```
    

- Installing the New NVIDIA Driver
    - Install Prerequisite Packages for NVIDIA Driver
    
    ```jsx
    $ sudo apt install ubuntu-drivers-common
    $ sudo add-apt-repository ppa:graphics-drivers/ppa
    $ sudo apt update
    $ sudo apt install alsa-utils -y
    ```
    

- Install the graphics driver labeled as **"recommended"** after executing the command.
    - Example: Installing Driver for NVIDIA GeForce RTX 3060
    
    ```jsx
    $ sudo ubuntu-drivers devices
    
    == /sys/devices/pci0000:00/0000:00:03.1/0000:09:00.0 ==
    modalias : pci:v000010DEd00002504sv00001458sd0000407Bbc03sc00i00
    vendor   : NVIDIA Corporation
    model    : GA106 [GeForce RTX 3060 Lite Hash Rate]
    driver   : nvidia-driver-550-open - distro non-free
    driver   : nvidia-driver-545 - distro non-free
    driver   : nvidia-driver-535 - distro non-free
    driver   : nvidia-driver-535-server-open - distro non-free
    **driver   : nvidia-driver-550 - distro non-free recommended**
    driver   : nvidia-driver-545-open - distro non-free
    driver   : nvidia-driver-535-server - distro non-free
    driver   : nvidia-driver-535-open - distro non-free
    driver   : nvidia-driver-470 - distro non-free
    driver   : nvidia-driver-470-server - distro non-free
    driver   : xserver-xorg-video-nouveau - distro free builtin
    
    $ sudo apt install nvidia-driver-550
    
    # Please install the "recommended" driver as displayed on your own screen
    ```
    
- Reboot the OS after the graphics driver installation is complete.
    
    ```jsx
    $ sudo reboot
    ```
    

- After the OS starts, execute the **nvidia-smi** command to verify that the graphics driver is installed correctly.
    
    ```cpp
    $ nvidia-smi
    
    Tue Feb 25 09:47:42 2025       
    +-----------------------------------------------------------------------------------------+
    | NVIDIA-SMI 550.120                Driver Version: 550.120        CUDA Version: 12.4     |
    |-----------------------------------------+------------------------+----------------------+
    | GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
    | Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
    |                                         |                        |               MIG M. |
    |=========================================+========================+======================|
    |   0  NVIDIA GeForce RTX 3060        On  |   00000000:09:00.0 Off |                  N/A |
    |  0%   42C    P8             23W /  170W |       2MiB /  12288MiB |      0%      Default |
    |                                         |                        |                  N/A |
    +-----------------------------------------+------------------------+----------------------+
                                                                                             
    +-----------------------------------------------------------------------------------------+
    | Processes:                                                                              |
    |  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
    |        ID   ID                                                               Usage      |
    |=========================================================================================|
    |  No running processes found                                                             |
    +-----------------------------------------------------------------------------------------+
    ```
    

## **2. Gcube Agent Installation**

- Pre-installation Preparation for Gcube Agent
    1. Ensure all prerequisites are met before running the installation script.
        - [gcube.ai](http://gcube.ai/)  **Website Account**: Your login credentials for the official platform. 
        - **Email Address**: The email where you will receive essential configuration files and access tokens.
    2. Agent Installation File and Personal User Token Delivery <br>
    After Gcube receives your information, the Agent installation file and the Personal User Token required for installation will be sent to you.<br>
    **※ Note: These will be delivered to the email address you provided.**
        - gai_svr_inst: The executable installation file for the Gcube server.
        - Personal User Token: Your unique authentication key required during the setup process.
- Proceed with the installation after logging into Ubuntu.

- Create Agent Installation Directory and Grant Execution Permissions
    
    ```jsx
    # Create a dedicated directory
    $ mkdir -p ~/work/gcube_instller
    
    # Locate the Agent Installation File in the Dedicated Directory
    $ cd ~/work/gcube_installer/
    
    # Granting Execution Permission to the Agent Installation File
    $ chmod +x gai_svr_inst
    ```
    

- Basic File Installation
    
    ```jsx
    # Basic File Installation
    $ sudo ./gai_svr_inst base
    
    INFO[0000] Rnd initialized...                           
    INFO   [2025-02-25T06:11:15Z] Install Base All ...                         
    INFO   [2025-02-25T06:11:38Z] baseNetools complete.                        
    INFO   [2025-02-25T06:11:46Z] procWireGuard complete.                      
    INFO   [2025-02-25T06:11:46Z] PktPathBase: /root/packages/ubuntu22/ k8s_packages_u22_v1.28.tar.gz 
    INFO   [2025-02-25T06:12:10Z] procK8sPackage complete.                     
    ERROR  [2025-02-25T06:13:28Z] Failed to run                                 error="exit status 1"
    WARNING[2025-02-25T06:13:28Z] util.ExecCommand dpkg crio                    error="exit status 1"
    INFO   [2025-02-25T06:13:29Z] procCrio complete.                           
    INFO   [2025-02-25T06:14:31Z] procKubernetes complete.                     
    ERROR  [2025-02-25T06:14:36Z] Failed to run                                 error="exit status 100"
    WARNING[2025-02-25T06:14:36Z] ExecCommand apt install                       error="exit status 100"
    INFO   [2025-02-25T06:14:36Z] apt fix broken                               
    INFO   [2025-02-25T06:14:42Z] retry install nvidia-container-toolkit       
    INFO   [2025-02-25T06:14:52Z] procNvidiaPlugin complete.                   
    INFO   [2025-02-25T06:14:53Z] clearAutoUpdate complete.                    
    INFO   [2025-02-25T06:14:53Z] **procGaiClientInstaller complete.**  
    ```
    
    - When **procGaiClientInstaller complete** is displayed on the last line, it indicates that the installation of all core components has been successfully finished.
    
    - Terminal Output Example
    
    ![tier2 우분투 설치 가이드 에이전트 설치 예시 1 화면 이미지.png](img/tier-2-ubuntu-setting-guide/tier2%20우분투%20설치%20가이드%20에이전트%20설치%20예시%201%20화면%20이미지.png)
    

- Proceeding with Node Activation
    - Run the following command to finalize the node setup and initiate the service.
        - **Ethernet NIC Name**: The specific name of your network interface (e.g., eth0, enp3s0).
        - **Access Token**: Your unique personal token (Case-sensitive).
        
        ```jsx
        # View all Using Ethernet Interface

        $ ifconfig -a 
        ```

        ```jsx
        # Command to open Node

        $ sudo ./gai_svr_inst --nic <ethernet nic name> reg <access token>
        ```
        
        ```jsx
        # Execution Example
        # Verify active network interface name -> (enp5s0)
        
        $ ifconfig -a
        
        docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
                inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
                inet6 fe80::7807:f9ff:fe9c:6967  prefixlen 64  scopeid 0x20<link>
                ether 7a:07:f9:9c:69:67  txqueuelen 0  (Ethernet)
                RX packets 1779  bytes 49812 (49.8 KB)
                RX errors 0  dropped 0  overruns 0  frame 0
                TX packets 1189  bytes 130886 (130.8 KB)
                TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
        enp5s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
                inet 10.39.60.65  netmask 255.255.254.0  broadcast 10.39.61.255
                inet6 fe80::642:1aff:fe94:5edd  prefixlen 64  scopeid 0x20<link>
                ether 04:42:1a:94:5e:dd  txqueuelen 1000  (Ethernet)
                RX packets 2283880  bytes 2164088878 (2.1 GB)
                RX errors 0  dropped 10  overruns 0  frame 0
                TX packets 1513085  bytes 1359887094 (1.3 GB)
                TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
                device memory 0xfc400000-fc4fffff  
        
        lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
                inet 127.0.0.1  netmask 255.0.0.0
                inet6 ::1  prefixlen 128  scopeid 0x10<host>
                loop  txqueuelen 1000  (Local Loopback)
                RX packets 46784  bytes 3534359 (3.5 MB)
                RX errors 0  dropped 0  overruns 0  frame 0
                TX packets 46784  bytes 3534359 (3.5 MB)
                TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
        wlp4s0: flags=4098<BROADCAST,MULTICAST>  mtu 1500
                *ether f4:b3:01:39:2b:91  txqueuelen 1000  (Ethernet)*
                RX packets 0  bytes 0 (0.0 B)
                RX errors 0  dropped 0  overruns 0  frame 0
                TX packets 0  bytes 0 (0.0 B)
                TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
        ```
        
        ```jsx
        # Proceed to register Node by sudo ./gai_svr_inst --nic <ethernet nic name> reg <access token> 

        $ sudo ./gai_svr_inst --nic enp5s0 reg eyJh...생략...X63w
        
        INFO[0000] Rnd initialized...                           
        INFO   [2025-02-25T06:23:16Z] access token : &[eyJh...X63w] enp5s0 
        INFO   [2025-02-25T06:23:16Z] MAC address                                   mac="00:00:00:00:00:00"
        INFO   [2025-02-25T06:23:16Z] mac address 000000000000                     
        DEBUG  [2025-02-25T06:23:16Z] url https://api.gcube.ai/api/node/register   
        DEBUG  [2025-02-25T06:23:16Z] body {"category":"svr","macId":"000000000000"} 
        DEBUG  [2025-02-25T06:23:16Z] res &{200 6150125230709283 eyJh...xsHS  } 
        INFO   [2025-02-25T06:23:16Z] provision code 0000000000000000              
        INFO   [2025-02-25T06:23:16Z] start provision ...                          
        DEBUG  [2025-02-25T06:23:16Z] body {"provision_code":"0000000000000000"}
        ```
        
    
    - Execution Example
    
    ![tier2 우분투 설치 가이드 에이전트 설치 예시 2 화면 이미지.png](img/tier-2-ubuntu-setting-guide/tier2%20우분투%20설치%20가이드%20에이전트%20설치%20예시%202%20화면%20이미지.png)
    

- Verify Registered Nodes on the [gcube.ai](http://gcube.ai) Node Page
    - [Move to Node Page](https://gcube.ai/ko/provision/node/list)
    
    ![Setting_Guide_for_Tier_2_Node_Provider_20260105.jpg](img.en/Setting_Guide_for_Tier_2_Node_Provider_20260105.jpg)