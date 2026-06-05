# **gcube CLI — configure**

CLI 전역 설정을 조회하거나 변경합니다.

---

## **설정 관리**

```bash
gcube configure                              # 대화형 설정 (프롬프트가 순서대로 표시됩니다)
gcube configure set --token <토큰>           # API 토큰 저장
gcube configure set --platform-url <URL>     # 플랫폼 URL 변경 (기본값 사용 권장)
gcube configure set --ws-url <URL>           # WebSocket URL 변경 (기본값 사용 권장)
gcube configure set --output <형식>          # 기본 출력 형식 변경 (table|json|yaml)
gcube configure get token                    # 저장된 토큰 값 조회
gcube configure get platform-url             # 플랫폼 URL 조회
gcube configure get ws-url                   # WebSocket URL 조회
gcube configure get output                   # 현재 기본 출력 형식 조회
gcube configure status                       # 현재 설정 및 토큰 유효성 확인
```

!!! note
    `platform-url`과 `ws-url`은 기본값으로 gcube 공식 서버가 설정되어 있습니다. 별도의 프라이빗 환경을 사용하는 경우가 아니라면 변경할 필요가 없습니다.

!!! question "검토 필요"
    `platform-url`과 `ws-url`이 정확히 무엇인지, 어떻게 사용하는지 개발팀 확인이 필요합니다.

설정 파일은 `~/.gcube/config.yaml`에 저장됩니다.

```yaml
platform_url: https://api.gcube.ai
ws_url: wss://console.gcube.ai:61443
auth:
  access_token: "eyJ..."
  expires_at: "2026-07-01T00:00:00Z"    # 토큰 만료 일시
output: table
```

!!! note
    토큰이 만료되면 `gcube configure set --token <새 토큰>` 명령어로 토큰을 홈페이지에서 재발급 후 갱신하세요. 만료된 토큰으로 명령을 실행하면 종료 코드 `3`(인증 실패)이 반환됩니다.

!!! question "검토 필요"
    토큰 재발급 방법에 대한 구체적인 경로 및 절차 확인이 필요합니다.

---

## **출력 형식**

모든 커맨드에서 `-o` 글로벌 옵션으로 출력 형식을 지정할 수 있습니다.

```bash
gcube workload list               # table (기본)
gcube -o json workload list       # JSON
gcube -o yaml workload list       # YAML
gcube -o json workload describe 2212 | jq '.state'
```

!!! note
    위 예시의 `jq`는 JSON을 필터링하는 별도 CLI 도구입니다. 사전에 설치가 필요합니다.

    - macOS: `brew install jq`
    - Ubuntu/Debian: `sudo apt install jq`
    - Windows: [jq 공식 사이트](https://jqlang.github.io/jq/download/)에서 다운로드

!!! question "검토 필요"
    `jq` 사전 설치 필요 여부 및 gcube CLI와의 연동 방식 확인이 필요합니다.

기본 출력 형식을 변경하려면 아래 명령어를 사용하세요.

```bash
gcube configure set --output json
```

---

## **환경 변수**

환경 변수는 설정 파일보다 우선 적용됩니다 (`환경 변수 > 설정 파일 > 기본값`).

| 변수 | 설명 |
|---|---|
| `GCUBE_ACCESS_TOKEN` | Bearer 토큰 |
| `GCUBE_PLATFORM_URL` | 플랫폼 API URL |
| `GCUBE_OUTPUT` | 기본 출력 형식 (`table`\|`json`\|`yaml`) |

!!! note
    환경 변수는 주로 CI/CD 파이프라인(GitHub Actions, GitLab CI 등)에서 토큰을 코드에 직접 노출하지 않고 안전하게 전달할 때 사용합니다. 로컬 개발 환경에서는 `gcube configure set --token`을 사용하는 것이 일반적입니다.

GitHub Actions 사용 예시:

```yaml
- name: Register workload
  env:
    GCUBE_ACCESS_TOKEN: ${{ secrets.GCUBE_TOKEN }}
    GCUBE_OUTPUT: json
  run: gcube workload register -f pipeline.yaml
```

---

## **종료 코드**

| 코드 | 의미 |
|---|---|
| `0` | 성공 |
| `1` | 잘못된 인자 또는 상태 오류 |
| `2` | gcube API 오류 |
| `3` | 인증 실패 또는 토큰 만료 |
| `4` | 네트워크 오류 |

---

<div style="text-align: center;" markdown>
[다음: GPU 목록 조회 →](cli-gpu.ko.md){ .md-button .md-button--primary }
</div>

