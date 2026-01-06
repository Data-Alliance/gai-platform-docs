# **Troubleshooting Agent Errors**

![agent-error-01](img/troubleshooting_agent_errors/에이전트%20사용%20오류%20해결%20initializing%20오류.PNG)

If an "Initializing" error occurs, you should check if Hyper-V is enabled on your system.<br>

## **How to Enable Hyper-V**

![agent-error-02](img/troubleshooting_agent_errors/image02.png)

1\. Search for and run **"Turn Windows features on or off"** in the Windows search bar. <br><br>

![agent-error-03](img/troubleshooting_agent_errors/image03.png)

2\. Find **"Hyper-V"** in the list and check the box.

※ **Please note:** The Hyper-V feature is natively available only on **Windows Pro** (Professional) and Enterprise versions. <br><br>

![agent-error-04](img/troubleshooting_agent_errors/image04.png)

3\. Click **Restart** to reboot your system. <br><br>

## **Hyper-V Configuration After Reboot**

![agent-error-05](img/troubleshooting_agent_errors/image05.png)

1\. Search for **"Hyper-V Manager"** in the search bar and run the application. <br><br>

![agent-error-06](img/troubleshooting_agent_errors/image06.png)

2\. Right-click on your **computer name**, then select **"New"** > **"Virtual Machine"**. <br><br>

![agent-error-07](img/troubleshooting_agent_errors/image07.png)

3\. Set the **Name** and **Storage Location** for the virtual machine, then click **Next**.

※ **Note:** Since virtual Windows machines take up a significant amount of storage, it is recommended to designate a drive with **sufficient free space**. <br><br>

![agent-error-08](img/troubleshooting_agent_errors/image08.png)

4\. Select the **Generation** of the virtual machine. While **Generation 1** supports 32-bit versions of Windows, **Generation 2** supports only 64-bit versions of Windows.

※ **Note:** You cannot change the generation once it has been selected. If an issue occurs, you must delete the virtual machine and create a new one. <br><br>

![agent-error-09](img/troubleshooting_agent_errors/image09.png)

5\. Set the amount of **memory (RAM)** to allocate to the virtual machine. Choose a value based on your physical RAM capacity and the tasks you plan to perform within the virtual environment. (1GB = 1024MB) <br><br>

![agent-error-10](img/troubleshooting_agent_errors/image10.png)

6\. Next, enter the **location and size** of the virtual hard disk. Since the capacity can be expanded later, please set it based on your available physical hard disk space. 

※ **Example:** In this case, the laptop's disk was assigned as the D drive, and approximately half of its capacity was allocated. <br><br>

## **If the "Failed to change VM state" message appears, it means the initialization has failed.**

## **BIOS Settings**

How to Enter the BIOS

Turn on the power and immediately press the **[F2]** key repeatedly at high speed.

※ **Note:** On systems equipped with an SSD, the boot speed is extremely fast. Please start tapping the **[F2]** key immediately after pressing the power button.

BIOS Entry Methods by Manufacturer

| Manufacturer | BIOS Entry Key | Selecting Boot Priority Key | Site Links |
| --- | --- | --- | --- |
| Intel | F2 | F10 | [Link](https://www.intel.co.kr/content/www/kr/ko/homepage.html) |
| AMD | F2 | F10 | [Link](https://www.amd.com/ko/search.html) |
| MSI | DEL | F11 | [Link](https://kr.msi.com/support) |
| ASUS | F2 or Del | ESC or F8 or F12 | [Link](https://www.asus.com/kr/support/contact/troubleshooting/) |

※ The following instructions describe the BIOS setup process for **Intel systems**. Steps may vary depending on the manufacturer. For detailed assistance, if you encounter the Failed to change VM state (0x???????)error, please contact the manufacturer's support center with the specific **error code** shown in the parentheses.

### How to Enter Intel BIOS

![agent-error-11](img/troubleshooting_agent_errors/image11.png)

1\. Press the **[F2]** key as soon as the logo screen first appears during the boot process. <br>
2\. In the **Main** (or Basic) tab, change **Fast Boot** to **Disabled**. <br><br>

![agent-error-12](img/troubleshooting_agent_errors/image12.png)

3\. Return to the top-level menu. Press the **right arrow key** until the **Save & Exit** tab is displayed.<br>
4\. Select **Save Changes and Exit** (or **Save Changes and Reset**) to reboot the system with your changes applied.