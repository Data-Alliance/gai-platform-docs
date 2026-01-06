# **Stable Diffusion User Guide**
## **0. Prerequisites**

- What is Stable Diffusion?
    - An open-source generative AI model for Text-to-Image and Image-to-Image tasks
    - Designed to run on personal computers equipped with GPUs by significantly reducing computing resource requirements
    - Can be installed and executed in a **'local environment'** on a private PC, independent of an online connection <br><br>

- Gcube Sign-up and Point Purchase
    - Sign up on the Gcube official website([http://gcube.ai](http://gcube.ai/))
    
    ![Stable_Diffusion_20260106_01.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_01.jpg)
    
    ![Stable_Diffusion_20260106_02.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_02.jpg)
    
    - Log in and access User Mode
    
    ![Stable_Diffusion_20260106_03.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_03.jpg)
    
    - Click the **“Point Charge"** menu on the left sidebar
    
    ![Stable_Diffusion_20260106_04.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_04.jpg)
    
    - Select the desired amount of points to refill, and Choose a payment method and click the **“Payment”** button to complete the transaction.
    
    ![Stable_Diffusion_20260106_05.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_05.jpg)
    

## **1. gcube Platform Stable Diffusion Workload Preparation**

- Register a New Workload
    - After logging in, click the **“Create New Workload”** menu on the left sidebar
    
    ![Stable_Diffusion_20260106_06.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_06.jpg)
    

- - **Workload Information: Stable Diffusion Setup**
    - **Description:** Enter [ **Stable Diffusion** ] in the workload description field
    
    ![Stable_Diffusion_20260106_07.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_07.jpg)
    
    - **Container**: Configure the Container Image for Stable Diffusion
        - Storage Type: **Docker Hub**
        - Container Image : [ **universonic/stable-diffusion-webui** ]
            - Click the "Verify Image" button next to the input field. Most of the time, the container port will be automatically populated
        - Container Port: **8080** (Automatically configured)
    
    ![Stable_Diffusion_20260106_08.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_08.jpg)
    
    - GPU Selection : Configure the Execution Environment
        - Target Tier: **Tier 3** (Tier for individual users)
        - GPU Memory: **8GB**
        - GPU : **RTX 3070 X 1 10GB**
    
    ![Stable_Diffusion_20260106_09.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_09.jpg)
    
    - Options (Optional): Detailed Container Settings
        - **Replicas**: Set the number of identical container instances to run in parallel
        - **Minimum CUDA Version**: Specify the minimum CUDA version required by the container
        - **Shared Memory**: Specify the size of the shared memory available to the container
        - **※ Note : For this guide, we will proceed without configuring any optional settings**
    
    ![Stable_Diffusion_20260106_10.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_10.jpg)
    
    - Estimated Cost: Calculate the Expected Usage Fee
        - Click the checkbox next to **“Immediate Deploy”** to deploy immediately upon registration
        - Click the checkbox next to **“Manual Deploy”** to deploy manually after registration
        - Click the **“Register”** button to complete the workload registration
    
    ![Stable_Diffusion_20260106_11.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_11.jpg)
    

## **2. Running the Stable Diffusion Workload on Gcube Platform**

- Post-Registration Screen

![Stable_Diffusion_20260106_12.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_12.jpg)

- Verify the information of the created workload
    - Click on **“Stable Diffusion”** to view details
    
    ![Stable_Diffusion_20260106_13.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_13.jpg)
    
    - Scroll to the bottom of the Workload Details screen to check the **“Deploy Status”**
    
    ![Stable_Diffusion_20260106_14.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_14.jpg)
    
    - Ensure the Pod status in the Deployment Status section is **“Running”**
    - Click the **“Container Log”** button
    
    ![Stable_Diffusion_20260106_15.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_15.jpg)
    
    - Installation is complete when you see the message shown in the image within the logs
    - **※ Note: Installation time may vary depending on container settings and hardware specifications**
    
    ![gcube stable diffusion 사용 가이드 배포 상태 확인 이미지.PNG](img/stable-diffusion/gcube%20stable%20diffusion%20사용%20가이드%20배포%20상태%20확인%20이미지.PNG.png)
    
    - Return to the Workload Details screen and click the **“Service URL Link”**
    - **※ Note: If you click the link before confirming the container logs, the interface may not display correctly**
    
    ![Stable_Diffusion_20260106_16.jpg](img.en/Stable-diffusion/Stable_Diffusion_20260106_16.jpg)
    
    - If the screen below appears, Stable Diffusion has been successfully launched
    
    ![gcube stable diffusion 사용 가이드 실행 화면 이미지.PNG](img/stable-diffusion/gcube%20stable%20diffusion%20사용%20가이드%20실행%20화면%20이미지.PNG.png)
    

## **3. Stable Diffusion Execution Example on gcube Platform**

- Stable Diffusion Execution Example
    - Enter the prompt **"A cat in a Hat"** in the txt2img input field and click the **"Generate"** button
    
    ![gcube stable diffusion 사용 가이드 실행 예시 준비 이미지.PNG](img/stable-diffusion/gcube%20stable%20diffusion%20사용%20가이드%20실행%20예시%20준비%20이미지.PNG.png)
    
    - Confirm that an image similar to the one below is generated
    - **※ Note: Generated images may vary**
    
    ![gcube stable diffusion 사용 가이드 실행 예시 이미지.PNG](img/stable-diffusion/gcube%20stable%20diffusion%20사용%20가이드%20실행%20예시%20이미지.PNG.png)