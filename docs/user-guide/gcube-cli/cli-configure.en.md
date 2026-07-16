# **gcube CLI — configure**

View or change global CLI settings.

---

## **Configuration Management**

```bash
gcube configure                              # Interactive setup (prompts appear in order)
gcube configure set --token <token>          # Save API token
gcube configure set --platform-url <URL>     # Change platform URL (default recommended)
gcube configure set --ws-url <URL>           # Change WebSocket URL (default recommended)
gcube configure set --output <format>        # Change default output format (table|json|yaml)
gcube configure get token                    # View saved token value
gcube configure get platform-url             # View platform URL
gcube configure get ws-url                   # View WebSocket URL
gcube configure get output                   # View current default output format
gcube configure status                       # Check current settings and token validity
```

!!! note
    `platform-url` and `ws-url` are set to the official gcube server by default. There is no need to change them unless you are using a separate private environment.

The configuration file is saved at `~/.gcube/config.yaml`.

```yaml
platform_url: https://api.gcube.ai
ws_url: wss://console.gcube.ai:61443
auth:
  access_token: "eyJ..."
  expires_at: "2026-07-01T00:00:00Z"    # Token expiration time
output: table
```

!!! note
    If your token expires, reissue a new token from the website and update it with `gcube configure set --token <new token>`. Running commands with an expired token will return exit code `3` (authentication failure).

---

## **Output Format**

You can specify the output format using the `-o` global option on any command.

```bash
gcube workload list               # table (default)
gcube -o json workload list       # JSON
gcube -o yaml workload list       # YAML
gcube -o json workload describe 2212 | jq '.state'
```

!!! note
    `jq` in the example above is a separate CLI tool for filtering JSON. It must be installed beforehand.

    - macOS: `brew install jq`
    - Ubuntu/Debian: `sudo apt install jq`
    - Windows: Download from the [jq official site](https://jqlang.github.io/jq/download/)

To change the default output format, use the following command.

```bash
gcube configure set --output json
```

---

## **Environment Variables**

Environment variables take precedence over the configuration file (`environment variables > config file > defaults`).

| Variable | Description |
|---|---|
| `GCUBE_ACCESS_TOKEN` | Bearer token |
| `GCUBE_PLATFORM_URL` | Platform API URL |
| `GCUBE_OUTPUT` | Default output format (`table`\|`json`\|`yaml`) |

!!! note
    Environment variables are mainly used in CI/CD pipelines (GitHub Actions, GitLab CI, etc.) to securely pass tokens without exposing them directly in code. For local development, using `gcube configure set --token` is typical.

GitHub Actions usage example:

```yaml
- name: Register workload
  env:
    GCUBE_ACCESS_TOKEN: ${{ secrets.GCUBE_TOKEN }}
    GCUBE_OUTPUT: json
  run: gcube workload register -f pipeline.yaml
```

---

## **Exit Codes**

| Code | Meaning |
|---|---|
| `0` | Success |
| `1` | Invalid argument or state error |
| `2` | gcube API error |
| `3` | Authentication failure or token expired |
| `4` | Network error |

---

<div style="text-align: center;" markdown>
[Next: GPU List →](cli-gpu.en.md){ .md-button .md-button--primary }
</div>
