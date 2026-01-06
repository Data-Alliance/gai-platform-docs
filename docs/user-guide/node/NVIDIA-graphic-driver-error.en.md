# **Troubleshooting: NVIDIA Graphics Driver Recognition Error**

![NVIDIA 그래픽 드라이버 인식 오류 이미지.jpg](img/NVIDIA-graphic-driver-error/NVIDIA%20그래픽%20드라이버%20인식%20오류%20이미지.jpg)<br>

During the node provisioning process, the node status may be marked as **"Failed."**<br><br>

This issue often occurs when the operating system is running **multiple graphic drivers simultaneously.**<br><br>

For example, this conflict is common when both the **NVIDIA discrete GPU** and an **Integrated GPU (iGPU)**—such as AMD Radeon graphics or Intel HD graphics—are active at the same time.<br>

| ![amd raiden graphic driver 이미지.PNG](img/NVIDIA-graphic-driver-error/amd%20raiden%20graphic%20driver%20size%20down%20이미지.PNG) | ![nvidia graphic driver 이미지.PNG](img/NVIDIA-graphic-driver-error/nvidia%20graphic%20driver%20size%20down%20이미지.PNG) |

To ensure stable Gcube node operation, you must disable the integrated GPU (iGPU) to prevent driver conflicts and ensure the agent exclusively utilizes the required NVIDIA hardware.<br><br>

To resolve driver conflicts, use the **AMD Display Driver Uninstaller (DDU)** to completely remove the iGPU drivers, then proceed with the **Gcube Agent reinstallation.**<br><br>

Other troubleshooting methods include disabling the iGPU function in the BIOS, or identifying the iGPU in the Device Manager to disable the device and uninstall its driver.<br><br>

Once the conflicting graphics drivers are removed, the issue will be resolved and the status will be displayed as shown below.<br>
![NVIDIA 그래픽 드라이버 인식 오류 해결 이미지.png](img/NVIDIA-graphic-driver-error/NVIDIA%20그래픽%20드라이버%20인식%20오류%20해결%20이미지.png)