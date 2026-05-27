# **gcube CLI — credential**

Register and delete credentials for private container registries.

---

## **Registry Credential Management**

After registration, set `isCredential: true` in the workload YAML to apply it.

```bash
gcube credential list
gcube credential create --repo docker --username myuser --token mypassword
gcube credential delete --repo docker
```

!!! note "`--token` Value Types"
    The value entered for `--token` varies by registry.

    | Registry | `--token` Value |
    |---|---|
    | Docker Hub | Docker Hub account password or Access Token |
    | GitHub (`github`) | GitHub Personal Access Token (PAT) |
    | AWS ECR (`aws`) | IAM Secret Access Key |
    | Hugging Face | Hugging Face Access Token |

    After registration, you can verify saved credentials with `gcube credential list`.

AWS ECR requires an additional `--region` flag.

```bash
gcube credential create \
  --repo aws \
  --username <ACCESS_KEY_ID> \
  --token <SECRET_ACCESS_KEY> \
  --region ap-northeast-2
```

**Supported Registry Types (`--repo`):**

| Value | Registry |
|---|---|
| `docker` | Docker Hub |
| `github` | GitHub Container Registry |
| `harbor` | Harbor (on-premises container registry) |
| `aws` | AWS ECR |
| `huggingface` | Hugging Face |
| `quay` | Red Hat Quay |
