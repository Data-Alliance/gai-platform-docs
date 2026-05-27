# **gcube CLI — 시작하기**

gcube CLI는 gcube AI GPU 클라우드 플랫폼의 공식 커맨드라인 도구입니다. GPU 워크로드 등록·관리, 리소스 모니터링, 컨테이너 로그 스트리밍을 터미널에서 수행할 수 있습니다.

---

## **설치**

Python 3.10 이상이 필요합니다.

!!! note
    터미널(Windows: 명령 프롬프트 또는 PowerShell, macOS/Linux: Terminal)을 실행한 뒤 아래 명령어를 입력합니다.

!!! question "검토 필요"
    Windows 및 macOS/Linux 환경에서 정상 작동 여부를 확인해야 합니다.

```bash
pip install gcube-cli
gcube --version     # 설치가 정상적으로 완료되면 버전 번호가 출력됩니다
```

---

## **인증 설정**

1. [gcube 웹 콘솔](https://gcube.ai)에 로그인합니다.

2. **GCUBE 액세스 토큰 관리** 메뉴에서 토큰을 생성 후 복사합니다.

    !!! note
        웹 콘솔 로그인 후 우측 상단 사용자명 메뉴에서 "내 프로필" 클릭 → **GCUBE 액세스 토큰**에서 토큰을 발급할 수 있습니다.

3. 아래 명령어로 토큰을 설정합니다.

```bash
gcube configure set --token "eyJ..."    # eyJ... 부분을 복사한 실제 토큰으로 교체하세요
```

---

## **빠른 시작**

!!! note "CLI 표기 규칙"
    - `<꺽쇠>`로 감싼 값은 **필수 인자**입니다. 꺽쇠를 포함하지 않고 실제 값으로 교체해서 입력합니다.
      예: `<SER>` → `2212`
    - `[대괄호]`로 감싼 값은 **선택 옵션**입니다. 생략 가능합니다.
    - 명령어 끝의 `\`는 **줄 연속 문자**입니다. 하나의 명령어가 여러 줄에 걸쳐 있음을 나타내며, 실제로는 한 줄로 실행됩니다.

SER(Serial)은 워크로드에 자동 부여되는 고유 번호입니다. 등록 후 목록 조회나 로그 확인 시 사용합니다.

```bash
gcube configure set --token "eyJ..."          # 인증 토큰 설정
gcube gpu list                                 # 사용 가능한 GPU 및 CODE 확인
gcube workload register \
  --description "my first workload" \
  --image ollama/ollama:latest \
  --gpu 029                                    # 워크로드 등록 → SER 발급
gcube workload list                            # SER 확인
gcube workload logs <SER>                      # 실시간 로그 확인 (종료: Ctrl+C)
```

---

## **커맨드 구조**

```
gcube [글로벌 옵션] <서비스> <액션> [옵션]
```

!!! note
    - `<서비스>`: 명령 대상 (예: `gpu`, `workload`, `resource`, `point`, `credential`, `configure`)
    - `<액션>`: 수행할 작업 (예: `list`, `register`, `describe`, `logs`, `delete`)
    - `[글로벌 옵션]`과 `[옵션]`은 선택 사항입니다.

!!! question "검토 필요"
    서비스 및 액션의 전체 목록과 정확한 사용 방법을 개발팀에 확인 후 보완이 필요합니다.

| 글로벌 옵션 | 설명 | 기본값 |
|---|---|---|
| `-o, --output <형식>` | 출력 형식: `table` \| `json` \| `yaml` | `table` |
| `-V, --version` | 버전 표시 | — |
| `--help` | 도움말 | — |
