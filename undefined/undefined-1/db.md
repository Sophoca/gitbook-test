# Installation DB Environment Preparation Guide

{% hint style="info" %}
**Notice**

This guide is intended for infrastructure administrators at customer organizations.
{% endhint %}

---

## System Requirements

### 1. Hardware Requirements

| Item | Minimum Specification | Notes |
| --- | --- | --- |
| CPU | 2 Cores or more | - |
| Memory | 4GB or more | - |
| Disk | - | 3. Checking Disk (Volume) Requirements |

### 2. Operating System Requirements

| Item | Requirement |
| --- | --- |
| OS | Rocky Linux 9.5 or later |

### 3. Disk (Volume) Requirements

For TAC configurations, the following requirements must be met.

- All disks used in a TAC configuration must be **shared volumes accessible from all DB nodes**.

| Purpose | Requirement |
| --- | --- |
| Data / Archive / Redo | Prepare as a shared volume, raw device, or partitioned path<br>(do not create a file system) |
| Backup | Prepare as a shared volume with a file system path |

{% hint style="warning" %}
**Caution**

Since OwlDB automatically configures the Tibero-dedicated file system (TAS) on Data/Archive/Redo disks, you must not create partitioning or a file system in advance.
{% endhint %}

### 4. Kernel Parameter Configuration

The following kernel parameters must be configured to run the Tibero database. Configure them via '[Kernel Parameter Configuration](https://docs.tibero.com/tibero/topics/installation/installaion-guide/installation-prerequisites#undefined-4)' in the Tibero 'Installation Guide'.



## Network Requirements

### Required Port Configuration for Database Servers

The following ports are required for a new database installation.

| Port Type | Port Number | Purpose | Notes |
| --- | --- | --- | --- |
| **DB Listener Port** | Example)<br>8629/tcp | Database connection port | Allow inbound 8629 from the OwlDB server |
| **Inter-node Internal Connection Port** | Example)<br>8630~8679/tcp | Internal communication port between nodes in a TAC configuration <br>(+50 range based on the DB Listener port) | Allow both inbound and outbound between nodes (required only for TAC and DR configurations) |

{% hint style="warning" %}
**Caution**

**⚠️ Important — DB Listener Port Range Precautions**

The database uses ports in the **+50 range**based on the designated DB Listener port for inter-node internal connections.

**Example**: When the DB Listener port is 8629

- DB Listener port: 8629/tcp
- Inter-node internal connection ports: 8630/tcp ~ 8679/tcp (50 ports total)

Therefore, when configuring the DB Listener port, the entire +50 port range from that port must be free. No other applications or services may be using that port range, and port conflicts may cause database installation or TAC configuration to fail.
{% endhint %}

### Firewall Configuration

Firewall configuration is required for communication between the OwlDB server and the database server.



---

## Preparing and Placing Deployment Files

### 1. List of Required Files

- owldb dp binary (`owldb-dp-installer-*.tar.gz`)
- tibero binary (`tibero.tar.gz`)
- License file (`license.xml`)

### 2. Creating the Installation Directory

Create the path where the database will be installed (hereafter referred to as `설치 디렉터리`). (Example: `/home/rocky/owldb`)

```bash
mkdir -p {installation directory}/tibero
chmod 755 {installation directory}/tibero
```

`{설치 디렉터리}/tibero` The path is used as `$TB_HOME`in subsequent steps.

### **3. File Placement**

Extract the DP binary to `$TB_HOME`and place the tibero binary and license file.

```bash
# Extract DP binary
tar -zxvf owldb-dp-installer-%Y%m%d-%H.tar.gz -C $TB_HOME --strip-components=2

# Place tibero binary
mv {tibero binary file} $TB_HOME/tibero.tar.gz

# Place license file
mv {license file} $TB_HOME/license.xml
```

After preparation is complete, `$TB_HOME` the structure is as follows.

```
$TB_HOME/
 ├── tibero.tar.gz                    # tibero binary
 ├── license.xml                      # license file
 └── owldb-dp-installer/
      ├── install/                    # Tibero installation script
      ├── validate_infra.sh           # infrastructure validation script
      ├── install_pkg.sh              # Tibero package installation script
      └── tbagent_dist_latest.tar.gz  # tbagent binary
```

Proceed to the [Database Server Agent Installation documentation](agent.md)and continue from there.
