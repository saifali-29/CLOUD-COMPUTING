# Type-1 Hypervisor - Proxmox VE

This folder has the screenshots and details of the Proxmox VE part of my hypervisor performance experiment.

## Requirements

- A server or PC with Proxmox VE already installed
- Browser to access the Proxmox web interface
- Ubuntu ISO file
- Internet connection (for installing Sysbench inside the VM)

## Machine Specification (VM)

| Parameter | Configuration |
|---|---|
| OS | Ubuntu |
| CPU | 2 vCPU |
| RAM | 2 GB |
| Disk | 20 GB |
| Network | bridge `vmbr0` |

## Procedure

1. Opened `https://<PROXMOX_SERVER_IP>:8006` in the browser.

2. Got a security warning because Proxmox uses a self-signed certificate, so clicked **Advanced** and then **Proceed**.

3. Logged in with the given credentials.

4. Clicked **Create VM** and set:
   - **Name:** `CC-Experiment1-Type1`
   - **OS:** Ubuntu ISO, storage `local`
   - **Disk:** 20 GB (`local-lvm`)
   - **CPU:** 1 socket, 2 cores (2 vCPU)
   - **Memory:** 2048 MiB (2 GB)
   - **Network:** bridge `vmbr0`

5. Started the VM and opened the Console.

6. Installed Ubuntu on the VM and logged in.

7. Checked the machine using:
   - `hostnamectl`
   - `lscpu`
   - `free -h`
   - `df -h`
   - `top`

8. Installed Sysbench and ran the CPU benchmark.

9. Checked CPU, memory, network and disk usage from the VM Summary page in Proxmox.

10. Shut down the VM using:
    ```bash
    sudo poweroff
    ```

## Commands Used

### System Information

```bash
hostnamectl
lscpu
free -h
df -h
top
sysbench cpu --cpu-max-prime=20000 run
sudo poweroff
sysbench cpu --cpu-max-prime=20000 run
