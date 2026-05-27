# **워크로드 등록하기**

컨테이너 이미지와 GPU를 선택해 워크로드를 등록합니다.

!!! tip
    워크로드는 gcube에서 GPU 자원을 사용하기 위한 기본 단위입니다. 
    컨테이너 이미지, GPU, 옵션을 설정해 등록합니다.

## **시작 전 확인사항**

- 포인트가 충분히 충전되어 있어야 합니다.
- 사용할 컨테이너 이미지의 URL을 미리 준비해두세요.

## **① 기본 정보 입력**

1. Workload Mode 좌측 메뉴에서 새 워크로드 등록을 클릭합니다.
![001_register-workload](img/register-workload/001_register-workload.png)
1. 워크로드 설명란에 이 워크로드의 용도를 간단히 작성합니다.
![002_register-workload](img/register-workload/002_register-workload.png)

## **② 컨테이너 설정**

![003_register-workload](img/register-workload/003_register-workload.png)

| **항목** | **설명** |
| --- | --- |
| 저장소 유형 | 컨테이너 이미지가 저장된 플랫폼 선택 |
| 컨테이너 이미지 | 저장소별 이미지 URL 입력 |
| 컨테이너 포트 | 이미지 검증 시 자동 입력 |
| 컨테이너 명령 | 컨테이너 실행 시 시작 명령어 (선택) |
| 컨테이너 환경변수 | 컨테이너 내부 환경변수 설정 (선택) |
| 개인 Storage | 백업용 개인 저장소 연결 (선택) |
| 저장소 인증 | 개인 저장소 이미지 사용 시 체크 |

**저장소별 이미지 URL 입력 형식**

| **저장소** | **입력 형식** | **예시** |
| --- | --- | --- |
| Docker Hub | username/repository:tag | ollama/ollama:latest |
| NVIDIA NGC | nvcr.io/nvidia/repository:tag | nvcr.io/nvidia/cuda:12.0.0-base-ubuntu22.04 |
| GitHub | ghcr.io/owner/repository:tag | ghcr.io/organization/app:1.0 |
| Red Hat Quay | quay.io/namespace/repository:tag | quay.io/redhat/ubi8:latest |
| Hugging Face | registry.hf.space/username/repository:tag | registry.hf.space/username/model-server:v1 |

이미지 URL을 올바르게 입력하면 녹색 체크 표시와 함께 포트가 자동 입력됩니다.<br> 유효하지 않은 이미지는 빨간색 표시가 나타납니다.

## **③ GPU 선택**

![004_register-workload](img/register-workload/004_register-workload.png)

| **항목** | **설명** |
| --- | --- |
| GPU 모델명 | 원하는 GPU 모델 검색 및 선택 |
| GPU 메모리 | 필요한 최소 VRAM 용량 설정 |
| 비용 | 시간당 최소~최대 비용 범위로 필터링 |
| 사용가능한 GPU만 보기 | 현재 즉시 사용 가능한 GPU만 표시 |
| 레플리카 | 사용 GPU 대수 설정 |

**Tier 구분 기준**

- Tier 1: 클라우드 사업자
- Tier 2: 전용 서버
- Tier 3: PC방, 개인

## **④ 옵션 설정**

![005_register-workload](img/register-workload/005_register-workload.png)

| **항목** | **설명** |
| --- | --- |
| Istio 프록시 사용 | 컨테이너 네트워크 트래픽 관리 프록시 사용 여부 |
| Istio L7 Consistent Hash | 동일 클라이언트 요청을 같은 Pod로 라우팅 |
| 최소 CUDA 버전 | 필요한 최소 CUDA 버전 지정 |
| 공유 메모리 | 프로세스 간 데이터 공유 영역 크기 |

## **⑤ 등록**

![006_register-workload](img/register-workload/006_register-workload.png)
1. 총 예상 금액을 확인합니다.
2. 즉시 배포 여부를 선택합니다.
3. 등록 버튼을 클릭하면 워크로드가 생성됩니다.

## **등록 예시 — Ollama**

!!! tip
    Ollama로 DeepSeek 모델을 실행하는 기본적인 워크로드 등록 예시입니다.

| **항목** | **입력값** |
| --- | --- |
| 워크로드 설명 | Ollama DeepSeek 실행 |
| 저장소 유형 | Docker Hub |
| 컨테이너 이미지 | ollama/ollama:latest |
| GPU | RTX 3090 이상 권장 (VRAM 16GB+) |
| 레플리카 | 1 |
| 즉시 배포 | ON |
