# **gcube CLI — workload**

Register, view, update, and delete workloads, and check logs.

!!! note "Workload · Pod · Container Relationship"
    These three concepts in gcube have the following hierarchical structure.

    ```
    Workload
    └── Pod (created based on replica count)
        └── Container (runs based on the number of registered containers)
    ```

    - **Workload**: A task unit that bundles GPU, container, and options together
    - **Pod**: A running instance created when a workload is deployed. Replica count = Pod count
    - **Container**: An individual process running inside a Pod. Multiple containers run per Pod in a multi-container setup

---

## **List / Detail View**

```bash
gcube workload list
gcube workload describe <SER>
gcube -o json workload describe <SER>
```

| Column | Description |
|---|---|
| SER | Unique workload identifier |
| DESCRIPTION | Name/description |
| CATEGORY | Type |
| GPU | GPU specs |
| STATE | Status (`deploy` / `stopped`, etc.) |

!!! note "Full STATE Values"

    | Value | Meaning |
    |---|---|
    | `deploy` | Running normally |
    | `stopped` | Stopped |
    | `pending` | Preparing for deployment |
    | `error` | Error occurred |

---

## **Register**

### **Register with Inline Flags (Single Container/GPU)**

Single container and single GPU configurations can be registered quickly using flags only.

```bash
gcube workload register \
  --description "inference service" \
  --image ollama/ollama:latest \
  --gpu 029 \
  --cuda 12040
```

| Flag | Description |
|---|---|
| `--description` | Workload name (2–80 characters) |
| `--image` | Container image |
| `--gpu` | GPU code (CODE value from `gcube gpu list`) |
| `--cuda` | CUDA version code (optional, refer to [CUDA Version Code Table](#cuda-version-codes)) |
| `--repo` | Registry (default: `docker.io`) |
| `--port` | Service port (default: auto-detected) |
| `--credential` | Use private registry authentication |

!!! note "`--image` Input Format"
    Docker images are entered in the format `registry/image-name:tag`.

    | Example | Description |
    |---|---|
    | `ollama/ollama:latest` | ollama image on Docker Hub, latest version |
    | `pytorch/pytorch:2.0` | pytorch image on Docker Hub, version 2.0 |
    | `ghcr.io/myorg/myapp:v1.0` | Image from GitHub Container Registry |

    If the tag (`:latest`, etc.) is omitted, `:latest` is applied automatically.

!!! note "`--cuda` Selection Criteria"
    Only specify this if your container image requires a specific CUDA version. If omitted, the default driver version of the selected GPU node is applied. Check the image documentation for the required CUDA version and refer to the [CUDA Version Code Table](#cuda-version-codes).

!!! note "`--port` Auto-Detection"
    If the image's Dockerfile has an `EXPOSE` directive, the port is auto-detected. If not detected or if a different port is needed, specify it manually.

---

### **Register with YAML File**

Use a YAML file for multi-container or multi-GPU configurations, or when there are many detailed settings such as environment variables.

The `--skeleton` flag outputs a YAML template with a basic structure. Save it to a file, edit it, and use it.

```bash
gcube workload register --skeleton > workload.yaml  # Generate template
# Edit workload.yaml
gcube workload register -f workload.yaml             # Register
```

**workload.yaml format:**

```yaml
description: "My ML Training Job"     # Required (2–80 characters)
cuda: "12040"                          # CUDA version code (optional)
sharedMemory: 1                        # Shared memory size (GB), must be less than GPU VRAM

containers:
  - containerImage: "pytorch/pytorch:2.0"
    repo: docker.io
    port: 0                            # 0 = auto-detect
    maxConnection: 4                   # Max concurrent HTTP connections
    containerCommand: "python train.py"
    isCredential: false                # Set to true for private registry
    containerEnvs:
      - EPOCHS: "100"
      - BATCH_SIZE: "32"

gpuSpecs:
  - gpuCode: "029"                     # CODE value from gcube gpu list
  #- gpuCode: "031"                    # Add for multi-GPU (heterogeneous GPU supported)
```

!!! note "YAML Field Descriptions"
    - `sharedMemory`: Size of shared memory (`/dev/shm`) between containers. May be insufficient with the default (64MB) for multi-process training such as PyTorch DataLoader. Set to less than GPU VRAM.
    - `maxConnection`: Maximum number of concurrent HTTP connections to the container.
    - `containerCommand`: If omitted, the default `CMD` or `ENTRYPOINT` defined in the image is executed.
    - `gpuSpecs`: Repeating entries creates a multi-GPU configuration. Repeating the same `gpuCode` uses multiple of the same model; using different `gpuCode` values creates a heterogeneous GPU combination.

**Supported Container Registries (`repo`):**

| Value | Registry |
|---|---|
| `docker.io` | Docker Hub |
| `ghcr.io` | GitHub Container Registry |
| `nvcr.io` | NVIDIA NGC |
| `quay.io` | Red Hat Quay |
| `registry.hf.space` | Hugging Face |

### **CUDA Version Codes**

| Code | CUDA Version |
|---|---|
| `12000` | 12.0 |
| `12020` | 12.2 |
| `12030` | 12.3 |
| `12040` | 12.4 |
| `12050` | 12.5 |
| `12060` | 12.6 |
| `12080` | 12.8 |
| `12090` | 12.9 |
| `13000` | 13.0 |

---

## **Update**

!!! note
    Only workloads in `stopped` status can be updated. To update a workload in `deploy` status, first stop it with `gcube workload stop <SER>`.

The `--skeleton` flag exports the current workload's structure in YAML format. Edit it and re-apply.

```bash
gcube workload update <SER> --skeleton > workload.yaml  # Export current config
# Edit workload.yaml
gcube workload update <SER> -f workload.yaml             # Apply changes
```

---

## **Start / Stop / Delete**

```bash
gcube workload start <SER>
gcube workload stop <SER>          # Confirmation prompt
gcube workload stop <SER> -y       # Stop without confirmation
gcube workload delete <SER>        # Confirmation prompt
gcube workload delete <SER> -y     # Delete without confirmation
```

!!! warning
    Data inside the container cannot be recovered after deletion. Back up your work data in advance.

---

## **Log Streaming**

View real-time logs from a workload in `deploy` status.

```bash
gcube workload logs <SER>
gcube workload logs <SER> --pod 0 --container 1
```

!!! note
    Press **Ctrl+C** to stop log streaming. Running this on a workload that is not in `deploy` status will return an error.

!!! note
    If there are multiple pods or containers, running without `--pod`/`--container` will display a selection list.

---

## **Pod List**

View the status of pods belonging to a workload.

```bash
gcube workload pods <SER>
```

Output example:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┓
┃ NAME                     ┃ STATUS  ┃ IP          ┃ START_TIME          ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━┩
│ dep2212-76db6545b6-vh68z │ Running │ 10.244.1.5  │ 2026-05-15 09:00:01 │
│ dep2212-76db6545b6-85zbb │ Running │ 10.244.1.6  │ 2026-05-15 09:00:04 │
└──────────────────────────┴─────────┴─────────────┴─────────────────────┘
```

---

<div style="text-align: center;" markdown>
[Next: Resource Monitoring →](cli-resource.en.md){ .md-button .md-button--primary }
</div>
