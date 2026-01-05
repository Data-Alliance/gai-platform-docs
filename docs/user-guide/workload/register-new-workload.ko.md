# **새 워크로드 등록**

gcube의 GPU 자원을 사용하기 위해, ‘새 워크로드 등록’이 필요합니다. <br><br>

![새워크로드 등록_20251210_01.png](img/register-new-workload/새워크로드%20등록_20251210_01.png)

1\. Deploy mode에서  “**새 워크로드 등록**” 메뉴를 클릭하세요.<br><br>

2\. 워크로드 등록 페이지에 각 항목을 입력합니다.<br>

![새워크로드 등록_20251210_02.png](img/register-new-workload/새워크로드%20등록_20251210_02.png)

- **워크로드 설명**: 워크로드의 용도와 특징을 간단히 작성합니다.

### **컨테이너**

![새 워크로드 등록 컨테이너 이미지](img/register-new-workload/새워크로드%20등록_20251210_03.png)

- **저장소 유형**: 컨테이너 이미지가 저장된 플랫폼을 선택하세요.
- **컨테이너 이미지**: 아래 저장소별 이미지 입력 형식을 참고하여 컨테이너 이미지 URL을 입력하세요.
- **컨테이너 포트** : 컨테이너에서 사용하는 네트워크 포트입니다. 이미지 검증 시 자동으로 입력됩니다.

```markdown
=== "Docker Hub"
    ```
    username/repository:tag
    ```
    예시: `ollama/ollama:latest`

=== "NVIDIA NGC"
    ```
    nvcr.io/nvidia/repository:tag
    ```
    예시: `nvcr.io/nvidia/cuda:12.0.0-base-ubuntu22.04`

=== "GitHub"
    ```
    ghcr.io/owner/repository:tag
    ```
    예시: `ghcr.io/organization/app:1.0`

=== "Red Hat Quay"
    ```
    quay.io/namespace/repository:tag
    ```
    예시: `quay.io/redhat/ubi8:latest`

=== "Hugging Face"
    ```
    registry.hf.space/username/repository:tag
    ```
    예시: `registry.hf.space/username/model-server:v1`

```

예시:

```
ollama/ollama:latest
```

**이미지 검증 확인**

- 정확한 이미지 URL을 입력하면 녹색 체크 표시가 나타나고 포트가 자동으로 입력됩니다.
- 유효하지 않은 이미지는 빨간색 체크 표시가 나타나며 포트가 입력되지 않습니다.

- **컨테이너 명령** : Dockerfile의 CMD 항목(컨테이너 실행 시 시작될 명령어)을 설정합니다.
- **컨테이너 환경변수** : Dockerfile의 ENV 항목(컨테이너 내부에서 사용할 환경변수)을 설정합니다.
- **개인 Storage** : 학습한 데이터를 백업할 수 있는 개인 저장소 정보를 설정합니다. 개인저장소는 저장소 관리를 통해 등록하여 사용할 수 있습니다.
- **저장소 인증** : 개인 저장소에 있는 컨테이너 이미지를 사용할 경우 체크합니다. 단, 저장소 관리를 통해 개인저장소 인증이 완료된 경우 사용할 수 있습니다.

### **GPU 선택**

![새워크로드 등록_20251210_04.png](img/register-new-workload/새워크로드%20등록_20251210_04.png)

워크로드 이용 시 사용할 목적 노드를 선택할 수 있으며, 사용가능한 GPU만 보기를 활성화할 경우 현재 사용가능한 GPU 목록만 조회할 수 있습니다. 또한 모델명, vRAM,  비용기준으로 GPU를 검색할 수 있습니다. 

- **GPU 모델명** : GPU 모델별 입력 시 공급 가능한 GPU 리소스 항목이 나타납니다. 각 노드의 정보 중 Tier 구분은 아래 기준에 따라 나뉘어집니다.
    - `Tier 1` : 클라우드 사업자
    - `Tier 2` : 전용 서버
    - `Tier 3` : PC방, 개인
- **GPU 메모리** : 필요한 GPU 메모리의 용량을 설정합니다. 설정값에 따라 사용 가능한 GPU가 필터링됩니다.
- **비용** : 시간당 최소 비용과 최대 비용을 입력 시 해당 구간에 일치하는 GPU 모델이 표시되며, 예산에 맞는GPU 모델을 선택할 수 있습니다.

### **옵션**

![새워크로드 등록_20251210_05.png](img/register-new-workload/새워크로드%20등록_20251210_05.png)

- **레플리카** : 배포할 컨테이너 인스턴스의 수를 지정합니다.
- **최소 CUDA 버전** : CUDA의 버전을 지정합니다.
- **공유 메모리** : 프로세스 간 데이터 공유를 위해 설계된 영역 크기를 설정합니다.

### **등록**

![새워크로드 등록_20251210_06.png](img/register-new-workload/새워크로드%20등록_20251210_06.png)

- 총 예상 금액을 확인하고 즉시배포 여부를 선택한 후 “**등록**” 버튼을 클릭하세요.<br><br>

![새워크로드 등록_20251210_07.png](img/register-new-workload/새워크로드%20등록_20251210_07.png)

3\. 워크로드가 생성되어 목록에서 확인하실 수 있습니다.