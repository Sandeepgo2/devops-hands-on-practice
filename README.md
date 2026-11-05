# DevOps Hands-on Practice Lab

## About This Project

This repository documents my hands-on practice and implementation of DevOps tools, cloud technologies, Linux administration, automation, CI/CD pipelines, containerization, infrastructure as code, Kubernetes and monitoring.

The objective is to build practical DevOps skills by implementing real-world scenarios in a Linux environment.

## Environment Setup

| Component          | Details            |
| ------------------ | ------------------ |
| Host OS            | Windows 10         |
| Virtualization     | Oracle VirtualBox  |
| Guest OS           | Ubuntu 22.04.5 LTS |
| Linux User         | deploy             |
| SSH Service        | OpenSSH Server     |
| SSH Port           | 22                 |
| SSH Authentication | SSH key setup      |

## Phase 1: Linux Server Administration

### 1. Ubuntu Installation

* Installed Ubuntu 22.04.5 LTS on Oracle VirtualBox.
* Configured VM resources.
* Installed VirtualBox Guest Additions.
* Configured shared clipboard.

### 2. Initial Server Health Checks

Executed basic Linux commands to understand server resources and configuration.

| Command               | Purpose                    |
| --------------------- | -------------------------- |
| `cat /etc/os-release` | Check OS version           |
| `free -h`             | Check memory utilization   |
| `df -h`               | Check disk utilization     |
| `nproc`               | Check available CPU cores  |
| `ip addr`             | Check network interfaces   |
| `hostname -I`         | Identify server IP address |
| `uptime`              | Check system uptime        |
| `top`                 | Monitor running processes  |

### 3. Linux Package Management

Updated Ubuntu packages and installed commonly used administration utilities.

```bash
sudo apt update
sudo apt upgrade -y
```

Installed utilities:

```bash
sudo apt install git curl wget vim tree htop net-tools unzip jq openssh-server ca-certificates -y
```

### 4. Linux User Management

Created a dedicated deployment user instead of performing regular activities using the root account.

```bash
sudo adduser deploy
sudo usermod -aG sudo deploy
```

Verified user and group information:

```bash
id deploy
groups deploy
whoami
```

### 5. SSH Configuration

Installed and verified the OpenSSH server.

```bash
sudo systemctl status ssh
sudo systemctl enable ssh
```

Checked SSH listening port:

```bash
sudo ss -tulnp | grep :22
```

Generated/configured SSH keys and verified local SSH connectivity.

```bash
ssh localhost
```

Successfully connected to the Ubuntu server using SSH.

## Current Progress

* [x] Ubuntu installation
* [x] VirtualBox Guest Additions
* [x] Linux initial health checks
* [x] Package installation and updates
* [x] Dedicated deployment user creation
* [x] SSH server installation
* [x] Local SSH connectivity
* [ ] Verify SSH public-key authentication
* [ ] Configure SSH connectivity between two Linux servers
* [ ] Linux troubleshooting exercises

## Upcoming Implementation

1. Linux administration and troubleshooting
2. Git and GitHub workflows
3. Jenkins CI/CD pipeline implementation
4. Docker image creation and deployment
5. AWS infrastructure provisioning using Terraform
6. Kubernetes and Minikube
7. Prometheus and Grafana monitoring
8. Centralized logging
9. Shell and Python automation
10. End-to-end DevOps project

## Learning Approach

Every implementation will include:

* Practical implementation steps
* Commands and configuration
* Real-world use cases
* Troubleshooting scenarios
* Screenshots or architecture diagrams where useful

This repository will be continuously updated as I implement and complete each activity.


## Latest Progress – 05 November 2026

- Completed Linux CPU and memory monitoring.
- Practiced system load monitoring using uptime and vmstat.
- Reviewed resource-intensive processes.
- Documented Linux troubleshooting activities.
