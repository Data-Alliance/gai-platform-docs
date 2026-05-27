# **Workload SSH Terminal Access**

Connect directly to a deployed workload container via SSH.

!!! tip
    SSH terminal access allows you to run commands directly inside the container.
    You can download models, install packages, check logs, and more.

---

## **Before You Begin**

- The workload must be in **Deployed** status.
- Choose one of the two connection methods below.

| Method | Description |
|---|---|
| Built-in Terminal SSH | No installation required. Supports Windows 10 build 1809 or later, macOS, and Linux |
| External SSH Client | GUI-based program for users who are not familiar with terminals |

---

## **Check Connection Info**

1. Click the workload you want to connect to in the workload list to go to its detail page.

    ![Screenshot: Workload detail screen](img/ssh-terminal/001_워크로드_세부_정보_화면.png)

2. Confirm the pod status is **Running** in the **Deployment Status** tab.

    ![Screenshot: Pod running status confirmation](img/ssh-terminal/002_파드_상태_실행_확인_화면.png)

3. Click the **Container SSH** button.

    ![Screenshot: Container SSH button](img/ssh-terminal/003_컨테이너_SSH_버튼_화면.png)

4. Look up your public IP and register the connection info.

    ![Screenshot: Container SSH access](img/ssh-terminal/004_컨테이너_SSH_접속_화면.png)

5. Check the following information in the SSH connection info popup.

    | Item | Description |
    |---|---|
    | SSH Access Address | Domain address used for SSH connection |
    | SSH Access Port | SSH connection port number |
    | Public IP Address | Server public IP address |
    | Username | SSH login account name |
    | Password | SSH login password |

    ![Screenshot: SSH connection info popup](img/ssh-terminal/005_SSH_접속_정보_팝업_화면.png)

    !!! warning
        If the public IP address changes, delete the connection info and re-register the public IP.

---

## **How to Connect via SSH**

### **Method 1 — Built-in Terminal SSH (Windows / macOS / Linux)**

1. Open a terminal (Command Prompt, PowerShell, or Terminal) and enter the following command.

    ```bash
    ssh [username]@[SSH access address] -p [SSH access port]
    ```

    Example:
    ```bash
    ssh us306ef_4bjk6@entry.gcube.ai -p 34000
    ```

2. Enter your password to complete the connection. (The password will not be displayed as you type.)

    ![Screenshot: Terminal SSH connection complete](img/ssh-terminal/006_터미널_SSH_접속_완료_화면.png)

---

### **Method 2 — External SSH Client**

If you are not familiar with terminals, you can use a GUI-based external SSH client.
Commonly used programs are listed below.

| Program | Platform | Cost | Download |
|---|---|---|---|
| PuTTY | Windows | Free | [putty.org](https://www.putty.org) |
| MobaXterm | Windows | Free (Home Edition) | [mobaxterm.mobatek.net](https://mobaxterm.mobatek.net) |
| Bitvise SSH Client | Windows | Free | [bitvise.com](https://www.bitvise.com/ssh-client) |
| Termius | Windows / macOS / Linux | Free (Starter plan, some features require paid plan) | [termius.com](https://termius.com) |

!!! note "PuTTY Connection Example"
    1. Launch PuTTY.
    2. Enter the SSH access address (e.g., `entry.gcube.ai`) in **Host Name** and the SSH access port (e.g., `34000`) in **Port**.
    3. Set Connection type to **SSH** and click **Open**.
    4. Enter your username at `login as:`, then enter your password. (The password will not be displayed as you type.)

    ![Screenshot: PuTTY connection setup](img/ssh-terminal/007_PuTTY_접속_설정_화면.png)

    ![Screenshot: PuTTY login complete](img/ssh-terminal/008_PuTTY_로그인_완료_화면.png)

---

## **Post-Connection Usage Examples**

| Task | Command Example |
|---|---|
| Download AI model | `ollama pull deepseek-r1:8b` |
| Install package | `pip install [package name]` |
| Check container logs | `tail -f /var/log/[service name].log` |
| Check GPU status | `nvidia-smi` |
| Check processes | `ps aux` |

!!! warning
    Do not share your SSH credentials (password) externally. Connection info may change when the workload is redeployed.
