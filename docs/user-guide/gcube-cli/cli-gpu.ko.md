# **gcube CLI — gpu**

현재 사용 가능한 GPU 리소스를 조회합니다.

---

## **GPU 목록 조회**

```bash
gcube gpu list          # 현재 즉시 사용 가능한 GPU만 표시
gcube gpu list --all    # 사용 중이거나 공유 중지된 GPU를 포함한 전체 목록
```

출력 예시:

```
CODE  GPU_NAME    TIER   GPU  VRAM(GB)  CPU  MEM(GB)  DISK(GB)  PRICE/HR(₩)
001   rtxa2000    tier3  1    6         8    32        100       500 ~ 600
029   rtx3090     tier3  1    24        16   64        100       1,200 ~ 1,500
```

!!! note "컬럼 설명"
    - `CODE`: 워크로드 등록 시 `--gpu` 또는 `gpuCode`에 사용하는 GPU 식별 코드
    - `TIER`: GPU 공급자 유형 — `tier1` 클라우드 사업자 / `tier2` 전용 서버 / `tier3` 개인 PC
    - `PRICE/HR`: 범위로 표시되는 이유는 공급자가 설정한 가격이 노드마다 다를 수 있기 때문입니다. 실제 과금은 선택한 노드의 단가로 결정됩니다.

`CODE` 값은 워크로드 등록 시 `--gpu` 옵션 또는 YAML의 `gpuCode`로 사용합니다.

---

<div style="text-align: center;" markdown>
[다음: 워크로드 관리 →](cli-workload.ko.md){ .md-button .md-button--primary }
</div>