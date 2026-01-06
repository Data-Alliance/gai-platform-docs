# **Tier 2 Ubuntu OS Setup Guide**

Downloading Ubuntu Server 22.04 LTS and Creating a Bootable Drive <br>
    [Ubuntu Server 22.04 LTS Download](https://ubuntu.com/download/server/thank-you?version=22.04.5&architecture=amd64&lts=true)

- Running Ubuntu Server 22.04 LTS
    
    ![tier2 우분투 설치 가이드 첫 실행 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20첫%20실행%20화면%20이미지.PNG)
    

- Language Selection (English)
    
    ![tier2 우분투 설치 가이드 언어 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20언어%20설정%20화면%20이미지.PNG)
    

- Skip Installer Update
    
    ![tier2 우분투 설치 가이드 업데이트 거부 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20업데이트%20거부%20화면%20이미지.PNG)
    

- Keyboard Configuration(English)
    
    ![tier2 우분투 설치 가이드 키보드 언어 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20키보드%20언어%20설정%20화면%20이미지.PNG)
    

- Ubuntu Installation Type
    - **Ubuntu Server** Installation
    
    ![tier2 우분투 설치 가이드 우분투 타입 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20우분투%20타입%20설정%20화면%20이미지.PNG)
    

- During the installation, configure the network settings to ensure the OS can access the external internet. **(At least 100Mbps)**
    - **Verify that the IP address** is displayed next to DHCPv4 before proceeding.
    
    ![tier2 우분투 설치 가이드 네트워크 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20네트워크%20설정%20화면%20이미지.PNG)
    

- Configure Ubuntu Archive Mirror
    - Change the Mirror Address from the default address to **http://mirror.kakao.com/ubuntu**
    
    ![tier2 우분투 설치 가이드 미러 서버 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20미러%20서버%20설정%20화면%20이미지.PNG)
    

- Storage Configuration
    - Select **Custom Storage Layout** 
    
    ![tier2 우분투 설치 가이드 스토리지 설정 1 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%201%20화면%20이미지.PNG)
    
    - Select **free space** → **Add GPT Partition** 
    
    ![tier2 우분투 설치 가이드 스토리지 설정 2 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%202%20화면%20이미지.PNG)
    
    - Use the **entire space** of the target disk for OS installation.
        - [Allocate 2GB to **/boot** first]
        - [Assign all remaining capacity to the **/(root)** space]
    
    ![tier2 우분투 설치 가이드 스토리지 설정 3 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%204%20화면%20이미지.PNG)
    

- Profile Setup
    - Set the Ubuntu OS user account **ID and Password**
    - **※ It is recommended to save the ID/Password separately as they are required for future Agent installation.**
    
    ![tier2 우분투 설치 가이드 프로필 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20프로필%20설정%20화면%20이미지.PNG)
    

- Skip Ubuntu Pro Upgrade
    
    ![tier2 우분투 설치 가이드 ubuntu 업그레이드 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20ubuntu%20업그레이드%20화면%20이미지.PNG)
    

- SSH Setup
    - Check **"Install OpenSSH server"**.
    - Do not enter an SSH KEY.
    
    ![tier2 우분투 설치 가이드 OpenSSH Server 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20OpenSSH%20Server%20설정%20화면%20이미지.PNG)
    

- Featured Server Snaps
    - Do not select any additional software; proceed directly.
    - Select **"Done"** to finalize the installation.
    
    ![tier2 우분투 설치 가이드 기타 서버 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20기타%20서버%20설정%20화면%20이미지.PNG)
    

- Proceed with Installation and **Reboot** after completion.
