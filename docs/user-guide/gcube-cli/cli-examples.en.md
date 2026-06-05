# **gcube CLI — Usage Examples**

Practical examples of commonly used workflows.

---

## **Full ML Training Workload Flow**

A typical flow for selecting a GPU, registering a training job, and deleting the workload after completion.

```bash
# 1. Check available GPUs
gcube gpu list

# 2. Register workload (using YAML file)
gcube workload register --skeleton > train.yaml
# Edit train.yaml: set image, gpuCode, containerCommand, environment variables, etc.
gcube workload register -f train.yaml
# Workload registered. SER: 2212

# 3. Check deployment status and monitor logs
gcube workload describe 2212
gcube workload logs 2212

# 4. Check resource usage during training
gcube resource workload 2212

# 5. Check costs and delete after training completes
gcube point spending --workload 2212
gcube workload delete 2212 -y
```

---

## **Using Images from a Private Registry**

```bash
# 1. Register registry credentials
gcube credential create \
  --repo github \
  --username myusername \
  --token ghp_xxxxxxxxxxxx    # GitHub Personal Access Token

# 2. Set isCredential: true and repo: ghcr.io in workload.yaml, then register
gcube workload register -f workload.yaml
```

---

## **Checking Logs for a Multi-Container Workload**

```bash
# Running without flags will automatically display a Pod/container selection list
gcube workload logs 2226
# Workload 2226 has 2 pods, 2 containers each:
#   POD  NAME                STATUS   CONTAINERS
#   0    dep2226-xxx-aaa     Running  [0] myimage:v1
#                                     [1] sidecar:latest
#   1    dep2226-xxx-bbb     Running  [0] myimage:v1
#                                     [1] sidecar:latest

# Specify pod and container numbers to stream
gcube workload logs 2226 --pod 0 --container 1
```

---

If you encounter any issues or need additional support, visit the [gcube web console](https://gcube.ai) or contact the gcube support team at gcube.ai@data-alliance.com.

---

<div style="text-align: center;" markdown>
[Use Workloads →](../workload/workload-dashboard.en.md){ .md-button .md-button--primary }
[Run AI Models →](../platform-guide/ollama-api.en.md){ .md-button }
</div>
