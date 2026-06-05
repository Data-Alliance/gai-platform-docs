# **gcube CLI — 사용 예시**

자주 사용하는 작업 흐름을 모아둔 실전 예시입니다.

---

## **ML 학습 워크로드 전체 흐름**

GPU를 선택하고 학습 작업을 등록한 뒤, 완료 후 워크로드를 삭제하는 일반적인 흐름입니다.

```bash
# 1. 사용 가능한 GPU 확인
gcube gpu list

# 2. 워크로드 등록 (YAML 파일 사용)
gcube workload register --skeleton > train.yaml
# train.yaml 편집: image, gpuCode, containerCommand, 환경변수 등 설정
gcube workload register -f train.yaml
# Workload registered. SER: 2212

# 3. 배포 상태 확인 및 로그 모니터링
gcube workload describe 2212
gcube workload logs 2212

# 4. 학습 중 리소스 사용량 확인
gcube resource workload 2212

# 5. 학습 완료 후 비용 확인 및 삭제
gcube point spending --workload 2212
gcube workload delete 2212 -y
```

---

## **비공개 레지스트리 이미지 사용**

```bash
# 1. 레지스트리 인증 등록
gcube credential create \
  --repo github \
  --username myusername \
  --token ghp_xxxxxxxxxxxx    # GitHub Personal Access Token

# 2. workload.yaml에서 isCredential: true, repo: ghcr.io 설정 후 등록
gcube workload register -f workload.yaml
```

---

## **멀티 컨테이너 워크로드 로그 확인**

```bash
# 플래그 없이 실행하면 Pod/컨테이너 선택 목록이 자동 출력됨
gcube workload logs 2226
# Workload 2226 has 2 pods, 2 containers each:
#   POD  NAME                STATUS   CONTAINERS
#   0    dep2226-xxx-aaa     Running  [0] myimage:v1
#                                     [1] sidecar:latest
#   1    dep2226-xxx-bbb     Running  [0] myimage:v1
#                                     [1] sidecar:latest

# Pod·컨테이너 번호를 확인한 뒤 지정하여 스트리밍
gcube workload logs 2226 --pod 0 --container 1
```

---

문제가 발생하거나 추가 지원이 필요한 경우 [gcube 웹 콘솔](https://gcube.ai)을 방문하거나 gcube 지원팀(gcube.ai@data-alliance.com)에 문의해 주세요.

---

<div style="text-align: center;" markdown>
[워크로드 사용하기 →](../workload/workload-dashboard.ko.md){ .md-button .md-button--primary }
[AI 모델 실행하기 →](../platform-guide/ollama-api.ko.md){ .md-button }
</div>