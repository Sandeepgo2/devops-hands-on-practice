# Linux CPU and Memory Monitoring

## Objective

Understand how to monitor CPU and memory utilization on a Linux server and identify resource-consuming processes.

This activity simulates a real-world DevOps production troubleshooting scenario where an application server experiences performance degradation.

## Environment

* OS: Ubuntu 22.04.5 LTS
* Virtualization: Oracle VirtualBox
* CPU: 2 Virtual CPUs
* RAM: 4 GB allocated
* User: sandeepg

## 1. CPU Information

Command:

```bash
lscpu
```

Purpose:

Displays CPU architecture, CPU model, number of CPUs, cores, threads and virtualization details.

Observation:

* VM configured with 2 virtual CPUs.
* One NUMA node detected.
* CPU IDs: 0 and 1.

## 2. Memory Utilization

Command:

```bash
free -h
```

Observed output:

| Metric           | Value   |
| ---------------- | ------- |
| Total Memory     | 3.8 GiB |
| Used Memory      | 1.5 GiB |
| Free Memory      | 186 MiB |
| Buffer/Cache     | 2.1 GiB |
| Available Memory | 2.0 GiB |
| Total Swap       | 3.8 GiB |
| Used Swap        | 0       |

Analysis:

Although free memory is relatively low, approximately 2 GiB is available for applications.

Linux uses unused memory for filesystem caching. This memory can be reclaimed when applications require it.

Therefore, low free memory does not automatically indicate memory pressure.

Important: Always check the available memory rather than relying only on the free memory value.

## 3. Real-Time Process Monitoring

Command:

```bash
top
```

Purpose:

Displays real-time CPU utilization, memory utilization, running processes and process IDs.

Observed processes included:

* gnome-shell
* code (Visual Studio Code)
* Xwayland
* systemd-related processes

Analysis:

The higher CPU-consuming processes were primarily related to the Ubuntu desktop environment and VS Code.

This is expected because the VM runs Ubuntu Desktop rather than a minimal server installation.

Useful shortcuts inside top:

| Shortcut | Purpose                            |
| -------- | ---------------------------------- |
| P        | Sort by CPU usage                  |
| M        | Sort by memory usage               |
| 1        | Display individual CPU utilization |
| q        | Exit                               |

## 4. Identify Top CPU-Consuming Processes

Command:

```bash
ps aux --sort=-%cpu | head -10
```

Purpose:

Displays the top 10 processes sorted by CPU consumption.

For a cleaner output:

```bash
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head -10
```

## 5. Identify Top Memory-Consuming Processes

Command:

```bash
ps aux --sort=-%mem | head -10
```

Purpose:

Identifies processes consuming the highest amount of memory.

## 6. Important Linux Monitoring Commands

| Command    | Purpose                        |
| ---------- | ------------------------------ |
| lscpu      | CPU information                |
| free -h    | Memory utilization             |
| top        | Real-time process monitoring   |
| htop       | Interactive process monitoring |
| ps aux     | List running processes         |
| uptime     | System uptime and load average |
| vmstat 1 5 | System performance statistics  |
| df -h      | Disk utilization               |
| du -sh     | Directory size                 |

## 7. Production Troubleshooting Approach

When an application server experiences high CPU or memory utilization:

1. Check CPU information using lscpu.
2. Check available memory using free -h.
3. Monitor real-time processes using top.
4. Identify CPU-consuming processes.
5. Identify memory-consuming processes.
6. Check system load average using uptime.
7. Analyse system activity using vmstat.
8. Investigate the responsible application or service.
9. Take corrective action based on the root cause.

Never terminate a production process without identifying its purpose and assessing the impact.

## 8. Learning Outcome

Completed:

* Linux CPU information inspection.
* Memory utilization analysis.
* Real-time process monitoring.
* Identification of resource-consuming processes.
* Understanding Linux memory caching.
* Basic production troubleshooting methodology.

## Next Activities

* System load analysis using uptime.
* Performance monitoring using vmstat.
* Simulating high CPU utilization.
* Identifying and troubleshooting resource-intensive processes.
* Linux disk and filesystem monitoring.
