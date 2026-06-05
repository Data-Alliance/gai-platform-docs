# **gcube CLI — credential**

비공개 컨테이너 레지스트리의 인증 정보를 등록·삭제합니다.

---

## **레지스트리 인증 관리**

등록 후 워크로드 YAML에서 `isCredential: true`로 설정하면 적용됩니다.

```bash
gcube credential list
gcube credential create --repo docker --username myuser --token mypassword
gcube credential delete --repo docker
```

!!! note "`--token` 값 유형"
    `--token`에 입력하는 값은 레지스트리별로 다릅니다.

    | 레지스트리 | `--token` 값 |
    |---|---|
    | Docker Hub | Docker Hub 계정 비밀번호 또는 Access Token |
    | GitHub (`github`) | GitHub Personal Access Token (PAT) |
    | AWS ECR (`aws`) | IAM Secret Access Key |
    | Hugging Face | Hugging Face Access Token |

    등록 후 `gcube credential list`로 저장된 인증 정보를 확인할 수 있습니다.

AWS ECR은 `--region`이 추가로 필요합니다.

```bash
gcube credential create \
  --repo aws \
  --username <ACCESS_KEY_ID> \
  --token <SECRET_ACCESS_KEY> \
  --region ap-northeast-2
```

**지원 레지스트리 유형 (`--repo`):**

| 값 | 레지스트리 |
|---|---|
| `docker` | Docker Hub |
| `github` | GitHub Container Registry |
| `harbor` | Harbor (사내/온프레미스 컨테이너 레지스트리) |
| `aws` | AWS ECR |
| `huggingface` | Hugging Face |
| `quay` | Red Hat Quay |

---

<div style="text-align: center;" markdown>
[다음: 사용 예시 →](cli-examples.ko.md){ .md-button .md-button--primary }
</div>