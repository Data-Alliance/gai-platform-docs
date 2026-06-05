# **gcube CLI — Getting Started**

gcube CLI is the official command-line tool for the gcube AI GPU cloud platform. You can register and manage GPU workloads, monitor resources, and stream container logs from the terminal.

---

## **Installation**

Python 3.10 or higher is required.

!!! note
    Open a terminal (Windows: Command Prompt or PowerShell, macOS/Linux: Terminal) and enter the commands below.

!!! question "Review Needed"
    Verification is required to confirm proper operation on Windows and macOS/Linux environments.

```bash
pip install gcube-cli
gcube --version     # If installation is successful, the version number will be displayed
```

---

## **Authentication Setup**

1. Log in to the [gcube web console](https://gcube.ai).

2. Generate and copy a token from the **GCUBE Access Token Management** menu.

    !!! note
        After logging in to the web console, click your username in the upper right → click **"My Profile"** → issue a token under **GCUBE Access Token**.

3. Set the token with the following command.

```bash
gcube configure set --token "eyJ..."    # Replace eyJ... with your actual copied token
```

---

## **Quick Start**

!!! note "CLI Notation Rules"
    - Values wrapped in `<angle brackets>` are **required arguments**. Replace them with the actual value, without the brackets.
      Example: `<SER>` → `2212`
    - Values wrapped in `[square brackets]` are **optional**. They can be omitted.
    - A `\` at the end of a line is a **line continuation character**. It means the command continues on the next line and is executed as a single command.

SER (Serial) is a unique number automatically assigned to each workload. It is used when listing workloads or checking logs after registration.

```bash
gcube configure set --token "eyJ..."          # Set authentication token
gcube gpu list                                 # Check available GPUs and CODE
gcube workload register \
  --description "my first workload" \
  --image ollama/ollama:latest \
  --gpu 029                                    # Register workload → SER is issued
gcube workload list                            # Check SER
gcube workload logs <SER>                      # View real-time logs (exit: Ctrl+C)
```

---

## **Command Structure**

```
gcube [global options] <service> <action> [options]
```

!!! note
    - `<service>`: The target of the command (e.g., `gpu`, `workload`, `resource`, `point`, `credential`, `configure`)
    - `<action>`: The operation to perform (e.g., `list`, `register`, `describe`, `logs`, `delete`)
    - `[global options]` and `[options]` are optional.

!!! question "Review Needed"
    The full list of services and actions and their exact usage should be confirmed with the development team.

| Global Option | Description | Default |
|---|---|---|
| `-o, --output <format>` | Output format: `table` \| `json` \| `yaml` | `table` |
| `-V, --version` | Show version | — |
| `--help` | Show help | — |

---

<div style="text-align: center;" markdown>
[Next: Configuration Management →](cli-configure.en.md){ .md-button .md-button--primary }
</div>
