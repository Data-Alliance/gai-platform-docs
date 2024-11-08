# 새 워크로드 등록

gcube의 GPU를 공유받기 위해, ‘새 워크로드 등록’이 필요합니다. 

![register-new-workload](img/register-new-workload/register-new-workload.png)

1\. 워크로드 탭에서 “**새 워크로드 등록**” 버튼을 클릭하세요. <br><br>

2\. 워크로드 등록 페이지에 각 항목을 입력합니다.

### 설명
![input-workload-description](img/register-new-workload/workload_desc.png) <br>

- **워크로드 설명**: 워크로드의 용도와 특징을 간단히 작성합니다.


### 컨테이너
![input-workload-description](img/register-new-workload/workload_container.png) <br>

- **저장소 유형**: 컨테이너 이미지가 저장된 플랫폼을 선택하세요. <br>

- **컨테이너 이미지**: 아래 저장소별 이미지 입력 형식을 참고하여 컨테이너 이미지 URL을 입력하세요. 

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

!!! tip "이미지 검증 확인"
    * 정확한 이미지 URL을 입력하면 녹색 체크 표시가 나타나고 포트가 자동으로 입력됩니다
    * 유효하지 않은 이미지는 빨간색 체크 표시가 나타나며 포트가 입력되지 않습니다

<br>


- **컨테이너 명령**: 컨테이너가 시작될 때 실행할 명령어를 지정합니다. 컨테이너 내부에서 실행 가능한 명령어만 사용 가능합니다.

!!! warning "명령어 지정 시 주의사항"
    대부분의 경우, 이미지에 이미 기본 명령어가 설정되어 있으므로 비워두셔도 됩니다. <br>

    잘못된 명령어를 입력하면 <ins>컨테이너가 시작되지 않거나 즉시 종료</ins>될 수 있으니 주의하시기 바랍니다.

<br>

- **컨테이너 포트** : 컨테이너에서 사용하는 네트워크 포트입니다. 이미지 검증 시 자동으로 입력됩니다.

<br>

### 목적스펙
![input-workload-spec](img/register-new-workload/workload_spec.png) <br>

- **목적노드** : Tier별 공급 가능한 GPU 리소스 항목이 나타납니다. <br>
    - `Any` : 사용 가능한 GPU 자동 할당 <br>
    - `Tier 1` : 클라우드 사업자 <br>
    - `Tier 2` : 전용 서버 <br>
    - `Tier 3` : PC방, 개인 <br>
- **레플리카** : 배포할 컨테이너 인스턴스의 수를 지정합니다.<br>
- **GPU 메모리** : 필요한 GPU 메모리의 용량을 설정합니다. 설정값에 따라 사용 가능한 GPU가 필터링됩니다. <br>
- **GPU** : 메모리 요구사항에 맞는 사용 가능한 GPU 모델이 표시되며, 특정 모델을 선택할 수 있습니다. <br>

<br>

### 등록
![workload-registration](img/register-new-workload/workload_register.png) <br>

- 총 예상 금액을 확인하고 즉시배포 여부를 선택한 후 “**등록**” 버튼을 클릭하세요. <br>

<br>
![workload-registration-complete](img/register-new-workload/workload_registration_complete.png) <br>

3\. 워크로드가 생성되어 목록에서 확인하실 수 있습니다. 

