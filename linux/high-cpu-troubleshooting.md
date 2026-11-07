# Linux High CPU Utilization Troubleshooting

## 1. Objective

Understand how to identify, investigate and troubleshoot high CPU utilization on a Linux server using standard Linux monitoring commands.

## 2. Production Scenario

A production Linux server experiences unusually high CPU utilization, affecting application performance.

As a DevOps engineer, the objective is to identify the resource-intensive process, investigate the issue, resolve it and verify system recovery.

## 3. Initial System Health Check

Commands used:

```bash
uptime
top
ps aux --sort=-%cpu | head -10
```

Purpose:
- Check system uptime and load average.
- Monitor CPU and memory utilization.
- Identify processes consuming the highest CPU.

Initial observations:
- VM configured with 2 logical CPUs.
- CPU utilization was within normal operating range.
- VS Code and GNOME were among the resource-consuming processes.

## 4. Simulating High CPU Utilization

Command:

```bash
yes > /dev/null &
```

This starts a background process that continuously generates output and redirects it to `/dev/null`.

Identify the process PID:

```bash
echo $!
```

Observed PID: 8457

## 5. Identifying the High CPU Process

Commands:

```bash
top
```

```bash
ps aux --sort=-%cpu | head -10
```

Observed results:

| Parameter | Value |
|---|---|
| Process | yes |
| PID | 8457 |
| CPU utilization | Approximately 98–100% |
| Memory utilization | 0.0% |
| Process state | Running |

The `yes` process was identified as the primary CPU-consuming process.

## 6. Understanding System Load

Before terminating the process:

```text
Load average: 12.81, 7.69, 3.46
```

The load average represents the average number of tasks that are runnable or in uninterruptible sleep over 1, 5 and 15 minutes.

A high load average on a 2-CPU VM indicates elevated system load.

## 7. Resolving the Issue

Terminated the simulated process gracefully:

```bash
kill -TERM 8457
```

Verified whether the process was stopped:

```bash
ps -p 8457
```

The process was no longer running.

## 8. Post-Resolution Verification

Commands:

```bash
uptime
top
ps aux --sort=-%cpu | head -10
```

Observed CPU idle: 53.9% in the captured recovery snapshot.

The simulated process was no longer present in the process list.

The load average was still elevated because it is calculated over rolling time intervals and does not immediately return to normal.

## 9. Production Troubleshooting Approach

In a real production environment:

1. Check CPU utilization using `top`.
2. Identify resource-intensive processes.
3. Find the process PID.
4. Investigate the application or service associated with the process.
5. Review application logs.
6. Identify the root cause.
7. Apply an appropriate fix or restart the affected service.
8. Monitor CPU utilization after resolution.

Useful commands:

```bash
uptime
top
ps aux --sort=-%cpu | head -10
ps -p <PID> -o pid,ppid,stat,%cpu,%mem,etime,cmd
kill -TERM <PID>
```

## 10. Key Learnings

- How to monitor CPU utilization in Linux.
- How to identify resource-intensive processes.
- How to understand Linux load averages.
- How to investigate processes using PID.
- How to terminate a process gracefully.
- How to verify system recovery.

**Lab Status: Completed**
