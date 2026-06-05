# **gcube CLI — workload**

워크로드를 등록·조회·수정·삭제하고 로그를 확인합니다.

!!! note "워크로드 · Pod · 컨테이너 관계"
    gcube에서 세 개념은 다음과 같은 계층 구조를 가집니다.

    ```
    워크로드 (Workload)
    └── Pod (레플리카 수만큼 생성)
        └── 컨테이너 (등록한 컨테이너 수만큼 실행)
    ```

    - **워크로드**: GPU, 컨테이너, 옵션을 묶어 등록한 작업 단위
    - **Pod**: 워크로드가 배포될 때 생성되는 실행 인스턴스. 레플리카 수 = Pod 수
    - **컨테이너**: Pod 안에서 실행되는 개별 프로세스. 멀티 컨테이너 등록 시 Pod당 여러 개가 실행됨

---

## **목록 / 상세 조회**

```bash
gcube workload list
gcube workload describe <SER>
gcube -o json workload describe <SER>
```

| 컬럼 | 설명 |
|---|---|
| SER | 워크로드 고유 번호 |
| DESCRIPTION | 이름/설명 |
| CATEGORY | 유형 |
| GPU | GPU 스펙 |
| STATE | 상태 (`deploy` / `stopped` 등) |

!!! note "STATE 전체 값"

    | 값 | 의미 |
    |---|---|
    | `deploy` | 정상 실행 중 |
    | `stopped` | 중지 상태 |
    | `pending` | 배포 준비 중 |
    | `error` | 오류 발생 |

    !!! question "검토 필요"
        실제 STATE 값 전체 목록을 개발팀에 확인 후 보완이 필요합니다.

---

## **등록**

### **인라인 플래그로 등록 (단일 컨테이너/GPU)**

단일 컨테이너·단일 GPU 구성은 플래그만으로 빠르게 등록할 수 있습니다.

```bash
gcube workload register \
  --description "inference service" \
  --image ollama/ollama:latest \
  --gpu 029 \
  --cuda 12040
```

| 플래그 | 설명 |
|---|---|
| `--description` | 워크로드 이름 (2-80자) |
| `--image` | 컨테이너 이미지 |
| `--gpu` | GPU 코드 (`gcube gpu list`의 CODE 값) |
| `--cuda` | CUDA 버전 코드 (선택, [CUDA 버전 코드 표](http://127.0.0.1:8000/gai-platform-docs/user-guide/gcube-cli/cli-workload/#cuda) 참고) |
| `--repo` | 레지스트리 (기본: `docker.io`) |
| `--port` | 서비스 포트 (기본: 자동 감지) |
| `--credential` | 비공개 레지스트리 인증 사용 |

!!! note "`--image` 입력 형식"
    Docker 이미지는 `저장소/이미지명:태그` 형식으로 입력합니다.

    | 예시 | 설명 |
    |---|---|
    | `ollama/ollama:latest` | Docker Hub의 ollama 이미지, 최신 버전 |
    | `pytorch/pytorch:2.0` | Docker Hub의 pytorch 이미지, 2.0 버전 |
    | `ghcr.io/myorg/myapp:v1.0` | GitHub Container Registry의 이미지 |

    태그(`:latest` 등)를 생략하면 자동으로 `:latest`가 적용됩니다.

!!! note "`--cuda` 선택 기준"
    컨테이너 이미지에 특정 CUDA 버전이 필요한 경우에만 지정합니다. 생략하면 선택한 GPU 노드의 기본 드라이버 버전이 적용됩니다. 이미지 문서에서 요구 CUDA 버전을 확인한 뒤 [CUDA 버전 코드 표](http://127.0.0.1:8000/gai-platform-docs/user-guide/gcube-cli/cli-workload/#cuda)를 참고해 입력하세요.

!!! note "`--port` 자동 감지"
    이미지의 Dockerfile에 `EXPOSE` 지시어가 있으면 해당 포트가 자동으로 감지됩니다. 감지되지 않거나 다른 포트를 사용해야 하는 경우 직접 지정합니다.

---

### **YAML 파일로 등록**

멀티 컨테이너·멀티 GPU 구성이 필요하거나 환경변수 등 상세 설정이 많은 경우 YAML 파일을 사용합니다.

`--skeleton` 플래그는 기본 구조가 잡혀있는 YAML 템플릿을 출력합니다. 이를 파일로 저장한 뒤 편집하여 사용하세요.

```bash
gcube workload register --skeleton > workload.yaml  # 템플릿 생성
# workload.yaml 편집 후
gcube workload register -f workload.yaml             # 등록
```

**workload.yaml 형식:**

```yaml
description: "My ML Training Job"     # 필수 (2-80자)
cuda: "12040"                          # CUDA 버전 코드 (선택)
sharedMemory: 1                        # 공유 메모리 크기(GB), GPU VRAM 미만으로 설정

containers:
  - containerImage: "pytorch/pytorch:2.0"
    repo: docker.io
    port: 0                            # 0 = 자동 감지
    maxConnection: 4                   # 최대 동시 HTTP 접속 수
    containerCommand: "python train.py"
    isCredential: false                # 비공개 레지스트리 사용 시 true
    containerEnvs:
      - EPOCHS: "100"
      - BATCH_SIZE: "32"

gpuSpecs:
  - gpuCode: "029"                     # gcube gpu list의 CODE 값
  #- gpuCode: "031"                    # 멀티 GPU: 다른 gpuCode 추가 (이기종 GPU 가능)
```

!!! note "YAML 필드 보충 설명"
    - `sharedMemory`: 컨테이너 간 공유 메모리(`/dev/shm`) 크기입니다. PyTorch DataLoader 등 멀티프로세스 학습 시 기본값(64MB)이 부족할 수 있어 설정합니다. GPU VRAM 용량 미만으로 설정하세요.
    - `maxConnection`: 해당 컨테이너로 들어오는 최대 동시 HTTP 접속 수입니다.
    - `containerCommand`: 생략하면 이미지에 정의된 기본 `CMD` 또는 `ENTRYPOINT`가 실행됩니다.
    - `gpuSpecs`: 항목을 반복하면 멀티 GPU로 구성됩니다. 동일한 `gpuCode`를 반복하면 같은 기종 여러 대, 다른 `gpuCode`를 입력하면 이기종 GPU 조합이 됩니다.

**지원 컨테이너 레지스트리 (`repo`):**

| 값 | 레지스트리 |
|---|---|
| `docker.io` | Docker Hub |
| `ghcr.io` | GitHub Container Registry |
| `nvcr.io` | NVIDIA NGC |
| `quay.io` | Red Hat Quay |
| `registry.hf.space` | Hugging Face |

### **CUDA 버전 코드**

| 코드 | CUDA 버전 |
|---|---|
| `12000` | 12.0 |
| `12020` | 12.2 |
| `12030` | 12.3 |
| `12040` | 12.4 |
| `12050` | 12.5 |
| `12060` | 12.6 |
| `12080` | 12.8 |
| `12090` | 12.9 |
| `13000` | 13.0 |

---

## **수정**

!!! note
    `stopped` 상태인 워크로드만 수정할 수 있습니다. `deploy` 상태에서 수정하려면 먼저 `gcube workload stop <SER>`으로 중지한 뒤 진행하세요.

`--skeleton` 플래그를 사용하면 현재 워크로드의 기본 구조를 YAML 형식으로 내보낼 수 있습니다. 이를 편집한 뒤 다시 적용하세요.

```bash
gcube workload update <SER> --skeleton > workload.yaml  # 현재 설정 내보내기
# workload.yaml 편집 후
gcube workload update <SER> -f workload.yaml             # 수정 적용
```

---

## **시작 / 중지 / 삭제**

```bash
gcube workload start <SER>
gcube workload stop <SER>          # 확인 프롬프트
gcube workload stop <SER> -y       # 확인 없이 중지
gcube workload delete <SER>        # 확인 프롬프트
gcube workload delete <SER> -y     # 확인 없이 삭제
```

!!! warning
    워크로드 삭제 시 컨테이너 내부 데이터는 복구할 수 없습니다. 작업 데이터는 미리 백업하세요.

---

## **로그 스트리밍**

`deploy` 상태의 워크로드에서 실시간 로그를 확인합니다.

```bash
gcube workload logs <SER>
gcube workload logs <SER> --pod 0 --container 1
```

!!! note
    로그 스트리밍을 종료하려면 **Ctrl+C**를 누르세요. `deploy` 상태가 아닌 워크로드에서 실행하면 오류가 반환됩니다.

!!! question "검토 필요"
    Ctrl+C로 정상 종료되는지 확인이 필요합니다.

!!! note
    Pod·컨테이너가 여러 개인 경우 `--pod`/`--container` 없이 실행하면 선택 목록이 출력됩니다.

---

## **Pod 목록**

워크로드에 속한 Pod의 상태를 조회합니다.

```bash
gcube workload pods <SER>
```

출력 예시:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┓
┃ NAME                     ┃ STATUS  ┃ IP          ┃ START_TIME          ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━┩
│ dep2212-76db6545b6-vh68z │ Running │ 10.244.1.5  │ 2026-05-15 09:00:01 │
│ dep2212-76db6545b6-85zbb │ Running │ 10.244.1.6  │ 2026-05-15 09:00:04 │
└──────────────────────────┴─────────┴─────────────┴─────────────────────┘
```

---

<div style="text-align: center;" markdown>
[다음: 리소스 모니터링 →](cli-resource.ko.md){ .md-button .md-button--primary }
</div>