# Linux System Load and Performance Monitoring

## 1. Objective

Understand how to monitor Linux system load and performance using commands such as uptime, vmstat and ps.

This exercise simulates a real-world production scenario where users report slow application response times.

As a DevOps engineer, the objective is to identify whether the server is experiencing CPU contention, memory pressure or disk I/O bottlenecks.

## 2. Environment

* OS: Ubuntu 22.04.5 LTS
* Virtualization: Oracle VirtualBox
* CPU: 2 Virtual CPUs
* RAM: 4 GB allocated
* User: sandeepg

## 3. Check System Load Average

Command:

```bash
uptime
```

Purpose:

Displays system uptime, logged-in users and load averages.

Load average represents the average number of tasks in a runnable or uninterruptible state over three periods:

* Last 1 minute
* Last 5 minutes
* Last 15 minutes

Example:

```text
21:30:10 up 5 days, 2 users, load average: 0.45, 0.60, 0.75
```

Analysis:

The Ubuntu VM has 2 virtual CPUs.

A sustained load average above 2 deserves investigation. However, load average also includes tasks waiting for I/O, so it does not directly represent CPU utilization.

## 4. Monitor System Performance Using vmstat

Command:

```bash
vmstat 1 5
```

Purpose:

Displays system performance statistics at one-second intervals for five reports.

Important fields:

| Field | Description                               |
| ----- | ----------------------------------------- |
| r     | Processes waiting for CPU                 |
| b     | Processes blocked, often waiting for I/O  |
| swpd  | Virtual memory used                       |
| free  | Free memory                               |
| si    | Swap-in activity                          |
| so    | Swap-out activity                         |
| us    | CPU time spent executing user processes   |
| sy    | CPU time spent executing kernel processes |
| id    | CPU idle percentage                       |
| wa    | CPU I/O wait percentage                   |

Troubleshooting observations:

* High r values may indicate CPU contention.
* High b values may indicate blocked processes.
* Continuous si and so activity may indicate memory pressure.
* High wa may indicate storage or disk I/O bottlenecks.

These metrics should be investigated together rather than interpreted individually.

## 5. Identify CPU-Consuming Processes

Command:

```bash
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head -10
```

Purpose:

Displays the top 10 processes sorted by CPU utilization.

## 6. Identify Memory-Consuming Processes

Command:

```bash
ps -eo pid,comm,%cpu,%mem --sort=-%mem | head -10
```

Purpose:

Identifies processes consuming the highest amount of memory.

## 7. Production Troubleshooting Scenarios

| Observation              | Possible cause                       |
| ------------------------ | ------------------------------------ |
| High CPU utilization     | CPU-intensive application or process |
| High memory utilization  | Memory-intensive application         |
| Continuous swap activity | Memory pressure                      |
| High I/O wait            | Slow storage or disk bottleneck      |
| High load average        | CPU contention or I/O congestion     |

## 8. Production Troubleshooting Approach

When users report slow application performance:

1. Execute uptime to check system load.
2. Execute vmstat to analyse CPU, memory and I/O activity.
3. Identify resource-consuming processes using ps.
4. Investigate the application or service responsible.
5. Check application and system logs.
6. Identify the root cause.
7. Apply corrective action.
8. Monitor the server after remediation.

Never terminate a production process without understanding its purpose and assessing the impact.

## 9. Learning Outcomes

* Understanding Linux load average.
* Monitoring system performance using vmstat.
* Identifying CPU and memory-consuming processes.
* Understanding CPU contention and I/O wait.
* Learning basic Linux production troubleshooting techniques.

## 10. Next Activities

* Simulate high CPU utilization.
* Identify resource-intensive processes.
* Troubleshoot and resolve high CPU utilization.
* Linux disk and filesystem monitoring.
* Linux service management using systemctl.
* Log analysis using journalctl.
