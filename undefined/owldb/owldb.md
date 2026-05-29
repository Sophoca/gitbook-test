# Installation Guide / OwlDB Server Preparation and Installation / OwlDB Server Environment Preparation Guide

{% hint style="info" %}
**Note**

This guide is intended for customer infrastructure administrators.
{% endhint %}

---

## System Requirements

Verify that the server on which OwlDB will be installed meets the following requirements.

### 1. Hardware Requirements

| Item | Minimum Specification | Notes |
| --- | --- | --- |
| CPU | 2 Cores or more | - |
| Memory | 8 GB or more | - |
| Disk | 50 GB or more | Includes storage space for logs and backup files |

### 2. Software Requirements

OwlDB operates on a Docker-based architecture; therefore, the following software must be installed before proceeding with installation.

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

A minimum of 50 GB of disk space is required to install OwlDB. It is recommended to allocate space by purpose as described below.

| Area | Purpose | Recommended Size |
| --- | --- | --- |
| Installation Path | OwlDB binaries and configuration files | 10 GB |
| Data Path | Metadata storage | 20 GB |
| Log Path | OwlDB operational logs | 10 GB |
| Backup Path | Backup file storage | 10 GB |

---

## Network Requirements

The OwlDB server communicates with both user web browsers and each database server. Complete the following port configuration and communication allowance settings in advance.

### 1. OwlDB Server Port Configuration

The following ports must be open on the OwlDB server.

| Port | Purpose | Direction |
| --- | --- | --- |
| 80/tcp<br>(port configurable) | User web browser access | Allow inbound from user → OwlDB server |
| 40001/tcp | Communication with database servers | Allow inbound from database server → OwlDB server |

### 2. Firewall Configuration

Based on the port configuration above, firewall allow rules must be configured between the OwlDB server and the database servers. Set inbound and outbound rules in accordance with the customer environment's firewall policy.
