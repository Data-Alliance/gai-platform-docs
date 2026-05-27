# **gcube CLI — resource**

Query CPU, GPU, and memory usage of running workloads.

---

## **Resource Monitoring**

```bash
gcube resource workload <SER>
gcube -o json resource workload <SER>
```

Output example:

```
POD         TIME      GPU(%)  VRAM(%)  CPU(%)  MEM(%)  DISK(%)  NET_RX(kbps)  NET_TX(kbps)
pod-abc123  09:00:01  73.2    72.0     12.4    51.2    8.3      1,024         256
pod-def456  09:00:01  68.5    70.1     10.1    49.8    8.1      980           210
```
