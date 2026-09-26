Type-1 Hypervisor - Proxmox VE
This folder has the screenshots and details of the Proxmox VE part of my hypervisor performance experiment.

Requirements
A server or PC with Proxmox VE already installed
Browser to access the Proxmox web interface
Ubuntu ISO file
Internet connection (for installing Sysbench inside the VM)
Machine Specification (VM)
OS: Ubuntu
CPU: 2 vCPU
RAM: 2 GB
Disk: 20 GB
Network: bridge vmbr0
Procedure
Opened https://<PROXMOX_SERVER_IP>:8006 in the browser.
Got a security warning because Proxmox uses a self-signed certificate, so clicked Advanced and then Proceed.
Logged in with the given credentials.
Clicked Create VM and set:
Name: CC-Experiment1-Type1
OS: Ubuntu ISO, storage local
Disk: 20 GB (local-lvm)
CPU: 1 socket, 2 cores (2 vCPU)
Memory: 2048 MiB (2 GB)
Network: bridge vmbr0
Started the VM and opened the Console.
Installed Ubuntu on the VM and logged in.
Checked the machine using hostnamectl, lscpu, free -h, df -h and top.
Installed Sysbench and ran the CPU benchmark.
Checked CPU, memory, network and disk usage from the VM Summary page in Proxmox.
Shut down the VM using sudo poweroff.
Commands Used
sudo apt update
sudo apt install sysbench -y
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
hostnamectl
lscpu
free -h
df -h
top
sudo poweroff
Screenshots
lspuT.jpg - lscpu output (CPU details)
free -h (2).jpg - free -h output (memory usage)
SysbenchT1.jpg - Sysbench CPU test result
Result
Sysbench CPU test - sysbench cpu --cpu-max-prime=20000 run

CPU speed:

Events per Second: 1453.98
General statistics:

Total Time: 10.0030s
Total Number of Events: 14548
Latency (ms):

Minimum: 0.57
Average: 0.69
Maximum: 1.24
95th Percentile: 0.74
