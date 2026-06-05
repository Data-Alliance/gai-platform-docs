# **gcube CLI — resource**

실행 중인 워크로드의 CPU·GPU·메모리 사용량을 조회합니다.

---

## **리소스 모니터링**

```bash
gcube resource workload <SER>
gcube -o json resource workload <SER>
```

출력 예시:

```
POD         TIME      GPU(%)  VRAM(%)  CPU(%)  MEM(%)  DISK(%)  NET_RX(kbps)  NET_TX(kbps)
pod-abc123  09:00:01  73.2    72.0     12.4    51.2    8.3      1,024         256
pod-def456  09:00:01  68.5    70.1     10.1    49.8    8.1      980           210
```

---

<div style="text-align: center;" markdown>
[다음: 포인트 조회 →](cli-point.ko.md){ .md-button .md-button--primary }
</div>