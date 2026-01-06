# **Storage Management Setup**

Through Storage Management, you can configure container image repository and backup data storage information. <br><br>

![Storage_Management_Setting_20260106_01.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_01.jpg)

1\. Click the arrow next to your name → Click **“Storage Management”** <br><br>

![Storage_Management_Setting_20260106_02.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_02.jpg)

2\. As shown in the screen above, you can configure “Register Authentication” and “Connect Personal Backup Storage.” <br>

- **Register Authentication**: To use container images from a private repository when setting up a workload, you must register your repository credentials to access the image information.<br>
- **Connect Personal Backup Storage**: You can connect and save your trained data to a personal storage space.   <br><br>

![Storage_Management_Setting_20260106_03.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_03.jpg)

3\. Register Authentication: Click **“+ Register Authentication”** → Select the **“Repository”** provider → Enter the required information → Click the **“Register”** button to complete the process. <br><br>

![Storage_Management_Setting_20260106_04.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_04.jpg)

4\. Click the **“Edit”** button for user credentials → Modify the information in the pop-up window → Click the **“Register”** button to complete the modification. <br><br>

![Storage_Management_Setting_20260106_05.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_05.jpg)

5\. Connect Personal Backup Storage: Click **“+ Connect Personal Backup Storage”** → Select the **“Type”** in the storage registration pop-up → Enter the required information → Click the **“Register”** button to complete the process. <br><br>
6\. When registering storage information, set a Storage Alias to be displayed in the list and specify the Folder Path within the storage to be linked before saving.   <br>
[Example: “/data/data” is the path where Dropbox is mounted inside the container. You can read and write files at this location.] <br><br>

The access method and capacity can be adjusted as needed.

- dropbox<br>
    ![Storage_Management_Setting_20260106_06.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_06.jpg)
    
- aws s3<br>
[For AWS storage, you must enter the IAM access key, secret access key, and the bucket region.]  <br>
   ![Storage_Management_Setting_20260106_07.jpg](img.en/Storage-Management-Setting/Storage_Management_Setting_20260106_07.jpg)