# **NVIDIA 그래픽 드라이버 인식 오류**

![NVIDIA 그래픽 드라이버 인식 오류 이미지.jpg](img/NVIDIA-graphic-driver-error/NVIDIA%20그래픽%20드라이버%20인식%20오류%20이미지.jpg)<br>

노드 공급 중 상태가 노드 상태가 실패로 표기되는 오류가 발생할 수 있습니다.<br><br>

이런 현상은 OS에서 그래픽 드라이버가 2개 이상 구동하고 있을 시 발생할 수 있습니다.<br><br>

예시) NVIDIA와 IGPU(amd) 두 개의 그래픽 드라이버를 구동하고 있을 시<br>

| ![amd raiden graphic driver 이미지.PNG](img/NVIDIA-graphic-driver-error/amd%20raiden%20graphic%20driver%20size%20down%20이미지.PNG) | ![nvidia graphic driver 이미지.PNG](img/NVIDIA-graphic-driver-error/nvidia%20graphic%20driver%20size%20down%20이미지.PNG) |

gcube에서는 Nvidia 그래픽 카드만 받아들이고 있으므로 이 경우 iGPU(amd)를 삭제해야 합니다.<br><br>

amd 제조사 드라이버 삭제 유틸리티(DDU)로 iGPU 드라이버를 삭제한 뒤 gcube Agent 재설치를 진행합니다. <br><br>

이외 해결 방법으로 Bios에서 iGPU 기능 중지, 장치 관리자에서 iGPU 정보 확인 후 사용 중지 및 드라이버 삭제 등이 있습니다.<br><br>

Nvidia 이외의 그래픽 드라이버를 제거, Agent 재설치를 진행하신 후 노드를 실행하시면 아래와 같이 표기되며 해결됩니다.<br>
![NVIDIA 그래픽 드라이버 인식 오류 해결 이미지.png](img/NVIDIA-graphic-driver-error/NVIDIA%20그래픽%20드라이버%20인식%20오류%20해결%20이미지.png)