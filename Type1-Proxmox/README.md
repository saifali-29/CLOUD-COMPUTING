# Type-1 Hypervisor – Proxmox VE

## 1. Experiment Title

**Performance Evaluation of a Type-1 Hypervisor using Proxmox VE**

---

## 2. Objective

To install and configure an Ubuntu Virtual Machine (VM) on **Proxmox VE**, a Type-1 (bare-metal) hypervisor, and evaluate the virtual machine's CPU, memory, storage, and system performance using Linux system monitoring commands and the **Sysbench CPU benchmark**.

---

## 3. Hypervisor

**Hypervisor:** Proxmox VE
**Hypervisor Type:** Type-1 / Bare-Metal Hypervisor
**Web Interface:** `https://<PROXMOX_SERVER_IP>:8006`

Proxmox VE is a virtualization platform that runs directly on the physical server hardware and provides a web-based interface for managing virtual machines and containers.

---

## 4. Requirements

### Hardware / Software Requirements

* Server or PC with **Proxmox VE installed**
* Web browser
* Ubuntu ISO image
* Internet connection
* Proxmox VE web interface access
* Ubuntu VM
* Sysbench

---

## 5. Virtual Machine Configuration

| Parameter         | Configuration          |
| ----------------- | ---------------------- |
| VM Name           | `CC-Experiment1-Type1` |
| Guest OS          | Ubuntu                 |
| Hypervisor        | Proxmox VE             |
| CPU               | 2 vCPU                 |
| CPU Configuration | 1 Socket, 2 Cores      |
| RAM               | 2048 MiB (2 GB)        |
| Disk              | 20 GB                  |
| Disk Storage      | `local-lvm`            |
| Network           | `vmbr0`                |
| Network Type      | Bridged                |

---

## 6. Procedure

### Step 1: Access Proxmox VE

Opened the Proxmox VE web interface using:

```text
https://<PROXMOX_SERVER_IP>:8006
```

A browser security warning appeared because Proxmox uses a self-signed SSL certificate.

Selected:

**Advanced → Proceed**

and opened the Proxmox login page.

---

### Step 2: Login to Proxmox

Logged in to the Proxmox VE web interface using the provided credentials.

---

### Step 3: Create a Virtual Machine

Selected **Create VM** and configured the VM with the following parameters:

```text
Name: CC-Experiment1-Type1
OS: Ubuntu ISO
Disk: 20 GB
Storage: local-lvm
CPU: 1 Socket, 2 Cores
Memory: 2048 MiB
Network Bridge: vmbr0
```

---

### Step 4: Start the Virtual Machine

Started the newly created VM from the Proxmox web interface.

Opened the **Console** and proceeded with the Ubuntu installation.

---

### Step 5: Install Ubuntu

Installed Ubuntu inside the virtual machine and logged in after the installation was completed.

---

### Step 6: Check System Information

The following Linux commands were executed to inspect the VM configuration and resource usage:

```bash
hostnamectl
```

Displays information about the operating system and hostname.

```bash
lscpu
```

Displays CPU architecture and processor information.

```bash
free -h
```

Displays memory and swap usage in human-readable format.

```bash
df -h
```

Displays disk-space usage of mounted filesystems.

```bash
top
```

Displays real-time CPU, memory, process, and system activity.

---

## 7. Installing Sysbench

Updated the Ubuntu package repository:

```bash
sudo apt update
```

Installed Sysbench:

```bash
sudo apt install sysbench -y
```

Checked the installed Sysbench version:

```bash
sysbench --version
```

---

## 8. CPU Benchmark

The Sysbench CPU benchmark was executed using:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark performs CPU calculations using prime numbers and measures the processing performance of the virtual machine.

---

## 9. Sysbench CPU Benchmark Result

### CPU Performance

```text
CPU speed:

    Events per second: 1453.98
```

### General Statistics

```text
Total time:              10.0030s
Total number of events:  14548
```

### Latency

```text
Minimum:          0.57 ms
Average:          0.69 ms
Maximum:          1.24 ms
95th percentile:  0.74 ms
```

### Result Summary

| Metric            |        Result |
| ----------------- | ------------: |
| CPU Events/Second |   **1453.98** |
| Total Time        | **10.0030 s** |
| Total Events      |     **14548** |
| Minimum Latency   |   **0.57 ms** |
| Average Latency   |   **0.69 ms** |
| Maximum Latency   |   **1.24 ms** |
| 95th Percentile   |   **0.74 ms** |

---

## 10. System Monitoring

Resource utilization was monitored from both the Ubuntu VM and the Proxmox VE interface.

The following resources were observed:

* CPU utilization
* Memory utilization
* Disk utilization
* Network activity
* Running processes
* VM status

The Proxmox VM **Summary** page was used to observe the resource usage of the virtual machine.

---

## 11. Screenshots

The following screenshots are included as experimental evidence.

### 11.1 CPU Information

**File:** `lspuT.jpg`

Shows the output of:

```bash
lscpu
```

This screenshot contains CPU and processor information of the Ubuntu VM.

---

### 11.2 Memory Information

**File:** `free -h (2).jpg`

Shows the output of:

```bash
free -h
```

This screenshot shows the memory allocation and usage of the Ubuntu VM.

---

### 11.3 Sysbench CPU Benchmark

**File:** `SysbenchT1.jpg`

Shows the result of:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The screenshot contains the CPU speed, total execution time, number of events, and latency statistics.

---

## 12. Commands Used

All major commands used during the experiment are listed below:

```bash
sudo apt update

sudo apt install sysbench -y

sysbench --version

hostnamectl

lscpu

free -h

df -h

top

sysbench cpu --cpu-max-prime=20000 run

sudo poweroff
```

---

## 13. VM Shutdown

After completing the experiment, the Ubuntu VM was safely shut down using:

```bash
sudo poweroff
```

---

## 14. Result

An Ubuntu virtual machine was successfully created and executed on **Proxmox VE**, a Type-1 hypervisor.

The VM was configured with:

* **2 vCPUs**
* **2 GB RAM**
* **20 GB disk**
* **Bridged networking using `vmbr0`**

The Sysbench CPU benchmark produced:

```text
Events per Second: 1453.98
Total Time:         10.0030 s
Total Events:       14548
Average Latency:    0.69 ms
Maximum Latency:    1.24 ms
95th Percentile:    0.74 ms
```

These results provide a baseline for evaluating the CPU performance of the Ubuntu VM running on Proxmox VE.

---

## 15. Conclusion

The experiment successfully demonstrated the deployment and performance evaluation of a virtual machine using **Proxmox VE** as a Type-1 hypervisor.

The Ubuntu VM was successfully configured, system resources were monitored using Linux commands and the Proxmox VE dashboard, and CPU performance was measured using Sysbench.

The obtained benchmark results can be used for comparison with other hypervisor configurations in the overall hypervisor performance experiment.

---

## 16. Folder Structure

The experiment folder can be organized as follows:

```text
Type-1-Proxmox/
│
├── README.md
│
├── Screenshots/
│   ├── lspuT.jpg
│   ├── free -h (2).jpg
│   └── SysbenchT1.jpg
│
└── Results/
    └── Sysbench_CPU_Result.txt
```

---

## 17. Experiment Summary

| Category        | Details                       |
| --------------- | ----------------------------- |
| Experiment      | Type-1 Hypervisor Performance |
| Hypervisor      | Proxmox VE                    |
| Hypervisor Type | Type-1                        |
| Guest OS        | Ubuntu                        |
| CPU             | 2 vCPU                        |
| RAM             | 2 GB                          |
| Storage         | 20 GB                         |
| Network         | `vmbr0`                       |
| Benchmark       | Sysbench CPU                  |
| CPU Events/sec  | 1453.98                       |
| Average Latency | 0.69 ms                       |
| Maximum Latency | 1.24 ms                       |
