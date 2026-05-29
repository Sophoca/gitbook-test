# OwlDB Server Environment Preparation Guide

{% hint style="info" %}
**Notice**

This guide is intended for customer infrastructure administrators.
{% endhint %}

---

## System Requirements

Verify that the server on which OwlDB will be installed meets the following requirements.

### 1. Hardware Requirements

| Item | Minimum Specification | Notes |
| --- | --- | --- |
| CPU | 2 Cores or more | - |
| Memory | 8GB or more | - |
| Disk | 50GB or more | Includes storage space for logs and backup files |

### 2. Software Requirements

Since OwlDB operates on a Docker-based architecture, the following software must be installed before proceeding with the installation.

**Docker**

| Item | Requirement |
| --- | --- |
| Docker | 29.3.1 or later |
| Docker Compose | V2 (2.x) |

**Podman**

| Item | Requirement |
| --- | --- |
| Podman | 4.4 or later |
| Podman Compose | 1.2.0 or later |

### 3. Disk Configuration

A minimum of 50GB of disk space is required to install OwlDB. It is recommended to partition the space by purpose as described below.

| Area | Purpose | Recommended Size |
| --- | --- | --- |
| Installation Path | OwlDB binaries and configuration files | 10GB |
| Data Path | Metadata store | 20GB |
| Log Path | OwlDB operational logs | 10GB |
| Backup Path | Backup file store | 10GB |

---

## Network Requirements

The OwlDB server communicates with both users (web browsers) and each database server. Please complete the following port configuration and communication allowance settings in advance.

### 1. OwlDB Server Port Configuration

The following ports must be open on the OwlDB server.

| Port | Purpose | Direction |
| --- | --- | --- |
| 80/tcp<br>(port configurable) | User web browser access | Allow inbound: User → OwlDB server |
| 40001/tcp | Communication with database server | Allow inbound: Database server → OwlDB server |

### 2. Firewall Configuration

Based on the port configuration above, firewall allowance rules between the OwlDB server and database servers must be configured. Set inbound and outbound rules in accordance with the customer environment's firewall policy.
