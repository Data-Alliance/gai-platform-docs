# **모니터링 확인**

공유 중인 GPU의 실시간 성능 현황을 그래프로 확인합니다.

!!! tip
    모니터링 기능으로 GPU 사용률, 메모리, 네트워크 트래픽 등을 실시간 및 기간별로 확인할 수 있습니다.

## **모니터링 진입 방법**

1. 공유 중인 GPU 정보 화면에서 모니터링 버튼을 클릭합니다.
![001_check-monitoring](img/check-monitoring/001_check-monitoring.png)
1. 노드 모니터링 전체 현황 화면이 표시됩니다.
![002_check-monitoring](img/check-monitoring/002_check-monitoring.png)

## **확인 가능한 지표**

| **지표** | **단위** |
| --- | --- |
| GPU 사용량 | % |
| VRAM 사용량 | MB |
| CPU 사용량 | % |
| 메모리 사용량 | MB |
| 디스크 사용량 | MB |
| 네트워크 트래픽 (수신/송신) | Kbps |

## **시간 범위 설정**

1. 시간 범위 선택 버튼을 클릭하면 사전 정의된 시간대를 선택할 수 있습니다.
![003_check-monitoring](img/check-monitoring/003_check-monitoring.png)
1. 사용자 시간 범위를 선택하면 시작종료 시간을 직접 지정할 수 있습니다.
![004_check-monitoring](img/check-monitoring/004_check-monitoring.png)
1. 샘플링 간격 버튼으로 그래프 시간 단위를 조절합니다.

    | 기본값: 10분  | 최소: 1분 | 최대: 5시간 |
