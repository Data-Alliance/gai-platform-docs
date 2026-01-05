# **Tier 2 Ubuntu OS 세팅 가이드**

Ubuntu Server 22.04 LTS 이미지 파일 다운로드 및 부팅디스크 생성 <br>
    [Ubuntu Server 22.04 LTS 다운로드](https://ubuntu.com/download/server/thank-you?version=22.04.5&architecture=amd64&lts=true)

- Ubuntu Server 22.04 LTS 실행
    
    ![tier2 우분투 설치 가이드 첫 실행 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20첫%20실행%20화면%20이미지.PNG)
    

- 기본 언어 선택 (English)
    
    ![tier2 우분투 설치 가이드 언어 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20언어%20설정%20화면%20이미지.PNG)
    

- Installer Update 진행하지 않음
    
    ![tier2 우분투 설치 가이드 업데이트 거부 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20업데이트%20거부%20화면%20이미지.PNG)
    

- 키보드 설정(Korean)
    
    ![tier2 우분투 설치 가이드 키보드 언어 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20키보드%20언어%20설정%20화면%20이미지.PNG)
    

- Ubuntu 설치 타입 설정
    - **Ubuntu Server** 설치
    
    ![tier2 우분투 설치 가이드 우분투 타입 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20우분투%20타입%20설정%20화면%20이미지.PNG)
    

- 설치 시 OS 네트워크는, 외부 인터넷 연결이 가능하도록 설정 (최소 100Mbps 이상 권장)
    - DHCPv4 옆 **IP주소 표시 확인** 후 이동
    
    ![tier2 우분투 설치 가이드 네트워크 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20네트워크%20설정%20화면%20이미지.PNG)
    

- 미러 서버 설정
    - Mirror Address에 기본 주소 대신, **http://mirror.kakao.com/ubuntu** 로 변경
    
    ![tier2 우분투 설치 가이드 미러 서버 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20미러%20서버%20설정%20화면%20이미지.PNG)
    

- 스토리지 설정
    - **Custom Storage Layout** 선택
    
    ![tier2 우분투 설치 가이드 스토리지 설정 1 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%201%20화면%20이미지.PNG)
    
    - **free space** → **Add GPT Partition** 선택
    
    ![tier2 우분투 설치 가이드 스토리지 설정 2 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%202%20화면%20이미지.PNG)
    
    - OS 설치하려는 영역의 공간 **전부 사용**
        - [**/boot**에 2GB를 먼저 배정]
        - [나머지 용량을 모두 **/(루트)** 공간에 배정]
    
    ![tier2 우분투 설치 가이드 스토리지 설정 3 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20스토리지%20설정%204%20화면%20이미지.PNG)
    

- 프로필 설정
    - Ubuntu OS user 계정 **ID/PW** 설정
    - **※ ID/PW는 추후 Agent 설치 시 필요한 정보이므로 별도로 저장하는 것을 추천 드립니다.**
    
    ![tier2 우분투 설치 가이드 프로필 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20프로필%20설정%20화면%20이미지.PNG)
    

- Ubuntu Pro Upgrade **진행하지 않음**
    
    ![tier2 우분투 설치 가이드 ubuntu 업그레이드 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20ubuntu%20업그레이드%20화면%20이미지.PNG)
    

- SSH 서버
    - OpenSSH server **설치 체크**
    - SSH KEY는 입력하지 않음
    
    ![tier2 우분투 설치 가이드 OpenSSH Server 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20OpenSSH%20Server%20설정%20화면%20이미지.PNG)
    

- 기타 서버 설정
    - 기타 서버는 **미설치**
    
    ![tier2 우분투 설치 가이드 기타 서버 설정 화면 이미지.PNG](img/Ubuntu-OS-setup/tier2%20우분투%20설치%20가이드%20기타%20서버%20설정%20화면%20이미지.PNG)
    

- 이후 Install 진행 및 Install 완료 시 **재부팅 진행**
