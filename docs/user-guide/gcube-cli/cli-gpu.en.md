# **gcube CLI — gpu**

Query currently available GPU resources.

---

## **GPU List**

```bash
gcube gpu list          # Show only GPUs available for immediate use
gcube gpu list --all    # Show full list including in-use or sharing-stopped GPUs
```

Output example:

```
CODE  GPU_NAME    TIER   GPU  VRAM(GB)  CPU  MEM(GB)  DISK(GB)  PRICE/HR(₩)
001   rtxa2000    tier3  1    6         8    32        100       500 ~ 600
029   rtx3090     tier3  1    24        16   64        100       1,200 ~ 1,500
```

!!! note "Column Descriptions"
    - `CODE`: The GPU identifier used with `--gpu` or `gpuCode` when registering a workload
    - `TIER`: GPU provider type — `tier1` cloud provider / `tier2` dedicated server / `tier3` individual PC
    - `PRICE/HR`: Displayed as a range because the price set by each provider may vary per node. Actual billing is based on the rate of the selected node.

The `CODE` value is used with the `--gpu` option or `gpuCode` in YAML when registering a workload.

---

<div style="text-align: center;" markdown>
[Next: Workload Management →](cli-workload.en.md){ .md-button .md-button--primary }
</div>
