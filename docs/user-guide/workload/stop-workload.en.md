# **Stop Workload**

Stop a deployed workload.

!!! tip
    Stopping a workload halts point deductions.
    Make sure to save your data before stopping.

!!! warning
    If no backup storage is configured, all data and the environment from the running workload will be deleted upon termination.
    Set up Personal Storage in Storage Management beforehand.

## **How to Stop**

1. Click the Stop Deployment button for the workload you want to stop in the workload list.
![001_stop-workload.png](img/stop-workload/001_stop-workload.png)
2. Click the Confirm button in the confirmation popup.
3. The workload status will change from Deployed → Stopped and the service will be terminated.
![002_stop-workload.png](img/stop-workload/002_stop-workload.png)

## **How to Preserve Data After Stopping**

To preserve data after stopping a workload, you must connect Personal Storage in advance and configure it when registering the workload.

- Storage Management → Register personal backup storage connection
- When registering a workload → Select the storage under the Personal Storage field
