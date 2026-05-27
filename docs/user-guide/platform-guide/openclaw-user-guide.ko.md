# **gcube에서 OpenClaw 설치 및 실행하기**

gcube 워크로드 환경에서 Ollama 기반 gemma4:e4b 모델을 실행하고,<br> OpenClaw Gateway 및 Control UI를 구성하는 방법을 안내합니다.

## 시작 전 확인사항

이 가이드는 아래 순서로 진행됩니다.

1. 워크로드 생성 및 배포
2. SSH 접속
3. Ollama gemma4:e4b 모델 다운로드
4. Node.js 및 npm 설치
5. OpenClaw 설치 및 온보딩
6. 플러그인 의존성 설치
7. OpenClaw Gateway 실행
8. Telegram Pairing 승인
9. OpenClaw 프로세스 종료 및 확인
10. 웹 대시보드 접속
11. 설정 파일 확인 및 수정
12. 웹 대시보드 설정 및 활용
13. 문제 해결
14. 보안 주의사항

---

## 1단계 — 워크로드 생성 및 배포

아래 설정값으로 워크로드를 등록합니다.

| 항목 | 설정값 |
|---|---|
| 저장소 유형 | 도커허브 |
| 컨테이너 이미지 | `ollama/ollama:latest` |
| 컨테이너 포트 | `18789` |
| GPU 선택 | RTX Series |
| 기타 옵션 | 공유 메모리 4GB |

!!! note
    `18789` 포트는 **OpenClaw Gateway**와 **Control UI** 접속에 사용됩니다.

![워크로드 생성 화면](img/open-claw/001_gcube_워크로드생성.png)

---

## 2단계 — SSH 접속

워크로드가 실행되면 SSH 접속 정보를 확인합니다.

![SSH 접속 정보 화면](img/open-claw/002_SSH접속.png)

공인 IP를 조회해 등록한 뒤, SSH 접속 주소와 포트를 사용해 컨테이너에 접속합니다.

```bash
ssh <gcube에서 제공하는 SSH 접속 명령어>
```

PuTTY 터미널이 정상적으로 실행되면 아이디와 패스워드로 로그인합니다.

![PuTTY 접속 화면](img/open-claw/003_putty접속.png)

!!! tip
    PuTTY에서 붙여넣기는 **마우스 오른쪽 클릭**으로 할 수 있습니다.

---

## 3단계 — Ollama 모델 다운로드

아래 명령어를 입력해 `gemma4:e4b` 모델을 다운로드하고 실행합니다.

```bash
ollama run gemma4:e4b
```

![gemma4 모델 다운로드 화면](img/open-claw/004_젬마4모델다운로드.png)

!!! tip
    Ollama 채팅 화면에서는 `/bye` 명령어로 나갈 수 있습니다.

---

## 4단계 — Node.js 및 npm 설치

OpenClaw 설치를 위해 **Node.js, npm, git**을 설치합니다.

```bash
apt-get update && apt-get install -y curl git
curl -fsSL https://deb.nodesource.com/setup_lts.x | bash -
apt-get install -y nodejs
```

![패키지 업데이트 화면](img/open-claw/005_패키지업데이트.png)

설치 완료 후 아래 명령어로 정상 설치 여부를 확인합니다.

```bash
node -v
npm -v
git --version
```

---

## 5단계 — OpenClaw 설치 및 온보딩

```bash
npm i -g openclaw
openclaw onboard
```

![OpenClaw 설치 화면](img/open-claw/009_오픈클로설치.png)

![OpenClaw 온보드 화면](img/open-claw/010_오픈클로온보드.png)

---

## 6단계 — 플러그인 의존성 설치

`openclaw onboard` 실행 중 플러그인이 설치되지 않았다는 오류가 나오면<br> 아래 명령어로 필요한 의존성을 설치한 뒤 온보드를 다시 실행합니다.

```bash
npm i -g @larksuiteoapi/node-sdk nostr-tools
npm i -g @slack/web-api
npm i -g @whiskeysockets/baileys
```

```bash
openclaw onboard
```

![OpenClaw 온보드 재실행 화면](img/open-claw/011_오픈클로온보드.png)

!!! warning
    온보드 설정 중 `default model`에서는 정확한 **`gemma4:e4b`** 모델을 선택해야 합니다.

---

## 7단계 — OpenClaw Gateway 실행

온보드가 완료되면 Gateway를 실행합니다.

```bash
openclaw gateway
```

---

## 8단계 — Telegram Pairing 승인

OpenClaw Gateway가 실행되면 Telegram 연결 요청이 표시됩니다.<br> Telegram에서 확인한 Pairing Code를 사용해 승인 명령어를 실행합니다.

```bash
openclaw pairing approve telegram <PAIRING_CODE>
```

![Telegram Pairing 화면](img/open-claw/012_텔레그램페어링.png)

!!! warning
    Pairing Code는 외부에 노출하지 않도록 주의하세요.

---

## 9단계 — OpenClaw 프로세스 종료 및 확인

Gateway를 재실행해야 하는 경우 기존 프로세스를 종료한 뒤 다시 실행합니다.

```bash
pkill -9 -f openclaw
ps -ef | grep openclaw
openclaw gateway
```

---

## 10단계 — 웹 대시보드 접속

gcube 워크로드의 서비스 URL 또는 포트 접근 URL로 OpenClaw Control UI에 접속합니다.

```
http://<서비스_URL>:18789
```

![웹 대시보드 접속 화면](img/open-claw/013_웹대시보드접속.png)

---

## 11단계 — 설정 파일 확인 및 수정

아래 명령어로 `/root/.openclaw/openclaw.json` 설정 파일을 작성합니다.

!!! warning
    `<YOUR_GATEWAY_TOKEN>`, `<YOUR_TELEGRAM_BOT_TOKEN>`, `<서비스_URL>` 부분은 실제 사용하는 값으로 반드시 변경하세요.

```bash
cat > /root/.openclaw/openclaw.json <<'EOF'
EOF
```

```json
{
  "agents": {
    "defaults": {
      "workspace": "/root/.openclaw/workspace",
      "model": {
        "primary": "ollama/gemma4:e4b"
      },
      "models": {
        "ollama/gemma4:e4b": {}
      }
    }
  },
  "gateway": {
    "mode": "local",
    "auth": {
      "mode": "token",
      "token": "<YOUR_GATEWAY_TOKEN>"
    },
    "port": 18789,
    "bind": "lan",
    "controlUi": {
      "allowInsecureAuth": true,
      "allowedOrigins": [
        "http://<서비스_URL>:18789"
      ],
      "enabled": true,
      "dangerouslyDisableDeviceAuth": true
    },
    "tailscale": {
      "mode": "off",
      "resetOnExit": false
    },
    "nodes": {
      "denyCommands": [
        "camera.snap",
        "camera.clip",
        "screen.record",
        "contacts.add",
        "calendar.add",
        "reminders.add",
        "sms.send",
        "sms.search"
      ]
    },
    "tls": {
      "enabled": false,
      "autoGenerate": false
    }
  },
  "session": {
    "dmScope": "per-channel-peer"
  },
  "tools": {
    "profile": "coding",
    "web": {
      "search": {
        "provider": "ollama",
        "enabled": true
      }
    }
  },
  "plugins": {
    "entries": {
      "ollama": {
        "enabled": true
      },
      "telegram": {
        "enabled": true
      }
    }
  },
  "models": {
    "mode": "merge",
    "providers": {
      "ollama": {
        "baseUrl": "http://127.0.0.1:11434",
        "api": "ollama",
        "apiKey": "OLLAMA_API_KEY",
        "models": [
          {
            "id": "gemma4",
            "name": "gemma4",
            "reasoning": false,
            "input": ["text"],
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },
            "contextWindow": 128000,
            "maxTokens": 8192,
            "compat": { "supportsUsageInStreaming": true }
          },
          {
            "id": "gemma4:e4b",
            "name": "gemma4:e4b",
            "reasoning": true,
            "input": ["text", "image"],
            "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 },
            "contextWindow": 131072,
            "maxTokens": 8192,
            "compat": {
              "supportsTools": true,
              "supportsUsageInStreaming": true
            }
          }
        ]
      }
    }
  },
  "auth": {
    "profiles": {
      "ollama:default": {
        "provider": "ollama",
        "mode": "api_key"
      }
    }
  },
  "channels": {
    "telegram": {
      "enabled": true,
      "groups": {
        "*": { "requireMention": true }
      },
      "botToken": "<YOUR_TELEGRAM_BOT_TOKEN>"
    }
  },
  "wizard": {
    "lastRunAt": "2026-05-03T15:32:24.907Z",
    "lastRunVersion": "2026.5.2",
    "lastRunCommand": "onboard",
    "lastRunMode": "local"
  },
  "meta": {
    "lastTouchedVersion": "2026.5.2",
    "lastTouchedAt": "2026-05-03T15:32:25.021Z"
  }
}
```

---

## 12단계 — 웹 대시보드 설정 및 활용

gcube 워크로드의 서비스 URL 또는 포트 접근 URL로 접속 후 웹 대시보드를 확인합니다.

```
http://<서비스_URL>:18789
```

OpenClaw 웹 대시보드에서는 설정 확인 및 수정, 연결된 기능을 통해 OpenClaw를 직접 사용할 수 있습니다.

![OpenClaw 웹 대시보드 화면](img/open-claw/014_오픈클로웹대시보드.png)

---

## 13단계 — 문제 해결

| 문제 | 원인 | 해결 방법 |
|---|---|---|
| 웹 대시보드 접속 불가 | Gateway `bind` 설정이 외부 접속에 맞지 않음 | `bind` 값을 `lan`, `port` 값을 `18789`로 설정 |
| Control UI 접속 차단 | `controlUi.allowedOrigins` 설정이 서비스 URL과 다름 | `allowedOrigins`에 `http://<서비스_URL>:18789` 추가 |
| OpenClaw 명령어 실행 불가 | npm 전역 설치 경로 문제 | `npm i -g openclaw` 재실행 후 PATH 확인 |
| 플러그인 오류 발생 | 필요한 npm 패키지 누락 | 관련 패키지 전역 설치 |
| 모델 실행 실패 | Ollama 모델 미다운로드 | `ollama run gemma4:e4b` 실행 |
| Pairing 실패 | 요청 ID 또는 코드 불일치 | 최신 pairing 요청을 다시 확인 |

!!! note
    OpenClaw는 자주 업데이트되는 서비스이므로 명령어, 설정 항목, 화면 구성이 변경될 수 있습니다. <br>문서와 다른 문제가 발생하면 OpenClaw 공식 문서를 먼저 확인하세요.

---

## 14단계 — 보안 주의사항

!!! warning
    - Gateway Token은 외부에 공개하지 않습니다.
    - Telegram Bot Token은 문서에 직접 입력하지 않습니다.
    - Pairing Code와 Request ID는 사용 후 문서에서 제거합니다.
    - `allowedOrigins`에는 실제 사용하는 `http://<서비스_URL>:18789`만 입력합니다.
    - `allowInsecureAuth: true`, `dangerouslyDisableDeviceAuth: true`, `tls.enabled: false` 설정은 테스트 환경에서만 사용하는 것을 권장합니다.
