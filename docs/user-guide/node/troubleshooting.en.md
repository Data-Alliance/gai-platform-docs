# **Troubleshooting**

Common issues that occur during node operation and how to resolve them.

!!! tip
    If the issue is not resolved, contact gcube support at support@gcube.ai.

---

## **Agent-Related Errors**

### **Initializing Error**

![Agent error screen](img/troubleshooting/001_troubleshooting.PNG)

If an Initializing error occurs, check whether Hyper-V is enabled.

---

### **How to Enable Hyper-V**

1. Search for **"Turn Windows features on or off"** in the Windows search bar and open it.

    ![Turn Windows features on or off screen](img/troubleshooting/002_troubleshooting.png)

2. Find **"Hyper-V"** and check the box.

    ![Hyper-V checkbox screen](img/troubleshooting/003_troubleshooting.png)

    !!! warning
        The Hyper-V feature is only available by default on **Windows PRO** editions.

3. Click the **Restart** button to reboot.

    ![Reboot screen](img/troubleshooting/004_troubleshooting.png)

---

### **Hyper-V Configuration After Reboot**

1. Search for **"Hyper-V Manager"** in the search bar and open it.

    ![Hyper-V Manager screen](img/troubleshooting/005_troubleshooting.png)

2. Right-click your computer name and select **"New" → "Virtual Machine"**.

    ![Create virtual machine screen](img/troubleshooting/006_troubleshooting.png)

3. Set the virtual machine name and storage location, then click **Next**.

    ![Virtual machine name setup screen](img/troubleshooting/007_troubleshooting.png)

    !!! note
        Since virtual Windows installations can be large, it is recommended to choose a drive with sufficient free space.

4. Select the virtual machine generation.

    ![Virtual machine generation selection screen](img/troubleshooting/008_troubleshooting.png)

    | Generation | Description |
    |---|---|
    | Generation 1 | Supports 32-bit and 64-bit Windows installations |
    | Generation 2 | Supports 64-bit Windows installations only |

    !!! warning
        Once selected, the generation cannot be changed. If issues arise, delete and recreate the virtual machine.

5. Set the memory to allocate to the virtual machine. Consider your current RAM capacity and the tasks you plan to run. (1GB = 1024MB)

    ![Memory allocation screen](img/troubleshooting/009_troubleshooting.png)

6. Enter the location and size for the virtual hard disk. The capacity can be expanded later, so set it with your installed disk capacity in mind.

    ![Virtual hard disk setup screen](img/troubleshooting/010_troubleshooting.png)

---

## **Failed to Change VM State Error**

If the error `Failed to change VM state (0x???????)` appears, you need to enable virtualization in the BIOS. Contact your manufacturer with the error code shown in the parentheses.

---

### **BIOS Setup**

**Press the `F2` key rapidly multiple times immediately after powering on to enter BIOS.**

!!! note
    On devices with SSDs, the boot speed is very fast. Press the `F2` key repeatedly as soon as you power on.

**BIOS Entry Methods by Manufacturer**

| Manufacturer | BIOS Key | Boot Priority Key | Site |
|---|---|---|---|
| Intel | F2 | F10 | [Link](https://www.intel.com) |
| AMD | F2 | F10 | [Link](https://www.amd.com) |
| MSI | DEL | F11 | [Link](https://www.msi.com/support) |
| ASUS | F2 or Del | ESC or F8 or F12 | [Link](https://www.asus.com/support) |

### **Intel BIOS Setup**

1. Press the **F2** key when the logo screen first appears during boot.
2. In the main tab, change **Auto Boot** to disabled.

    ![BIOS auto boot setting screen](img/troubleshooting/011_troubleshooting.png)

3. Return to the top tab and press the right arrow key to navigate to the **Save & Exit** tab.
4. Select **Save Changes and Exit** to boot with the changes saved.

    ![BIOS save and exit screen](img/troubleshooting/012_troubleshooting.png)

---

## **NVIDIA Driver Recognition Error**

### **Symptom**

The node status may display as **'Failed'** while providing GPU sharing.

![NVIDIA driver recognition error screen](img/troubleshooting/013_troubleshooting.jpg)

### **Cause**

This can occur when **two or more graphics drivers** are running simultaneously on the OS.

Example: Running both NVIDIA and iGPU (AMD) graphics drivers at the same time.

![AMD iGPU driver screen](img/troubleshooting/014_troubleshooting.png)

Since gcube only supports NVIDIA graphics cards, the **iGPU (AMD) driver must be removed** in this case.

### **Resolution**

1. Use the AMD manufacturer's driver removal utility **(DDU)** to uninstall the iGPU driver.
2. **Reinstall the gcube Agent**.

!!! note "Other Solutions"
    - Disable iGPU in the BIOS
    - Find the iGPU in Device Manager and disable it, then uninstall the driver

After removing non-NVIDIA graphics drivers and reinstalling the Agent, the node will display correctly as shown below.

![NVIDIA driver recognition error resolved screen](img/troubleshooting/015_troubleshooting.png)

!!! warning
    If the issue persists, contact gcube support at support@gcube.ai.
