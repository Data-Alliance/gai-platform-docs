# **gcube CLI — point**

포인트 잔액과 사용 내역을 조회합니다.

---

## **포인트 조회**

```bash
gcube point status                           # 잔액 및 누적 사용량
gcube point spending                         # 당월 일별 사용 내역
gcube point spending --month 2026-03         # 특정 월 조회
gcube point spending --workload <SER>        # 워크로드 필터
```

`point status` 출력 예시:

```
Available Point:      50,000 P
Charged Point:       100,000 P
Spent Point:          50,000 P
Network Point:             0 P

Spending Summary:
  Total:             50,000 P
  Prev Month:        20,000 P
  This Month:        30,000 P
```

!!! note "포인트 항목 설명"

    | 항목 | 설명 |
    |---|---|
    | `Available Point` | 현재 사용 가능한 잔액 |
    | `Charged Point` | 누적 충전 총액 |
    | `Spent Point` | 누적 사용 총액 |
    | `Network Point` | 네트워크 트래픽 사용에 따라 차감되는 포인트 |

---

<div style="text-align: center;" markdown>
[다음: 레지스트리 인증 관리 →](cli-credential.ko.md){ .md-button .md-button--primary }
</div>