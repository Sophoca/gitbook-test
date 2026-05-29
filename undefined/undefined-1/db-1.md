# Registration DB Environment Preparation Guide

{% hint style="info" %}
**Note**

This guide is intended for customer infrastructure administrators.
{% endhint %}

{% hint style="info" %}
**Note**

To register and manage an existing Tibero instance in OwlDB, **Tibero version 7 or higher**is required.
{% endhint %}

---

## System Requirements

### Disk (Volume) Requirements

Since the existing database is already configured, no separate preparation is needed for Data/Archive/Redo disks. Only the Backup disk needs to be verified.

| Disk | Requirements |
| --- | --- |
| Backup | xfs filesystem creation and mount completed |

{% hint style="info" %}
**Note**

For TAC configurations, the Backup disk must be a shared volume accessible from all nodes.
{% endhint %}

## Network Requirements

### **Required Port Configuration for Database Servers**

The following ports are required to register an existing database with OwlDB.

| Port Type | Port Number | Purpose | Notes |
| --- | --- | --- | --- |
| **DB Listener **<br>**Port** | Existing DB Setting | Database connection port<br>Tibero: ex) 8629/tcp | Allow inbound DB Listener port<br>from the OwlDB server |

{% hint style="warning" %}
**Caution**

Do not change ports already in use by the existing database. Additionally open port 40001 for Agent communication and the Listener port for DB connectivity.
{% endhint %}

### Firewall Configuration

Firewall configuration is required for communication between the OwlDB server and the database server.



---

## Database Configuration Requirements

### Required Settings for TAC and DR Configurations

For databases operating in a TAC (Tibero Active Cluster) or DR configuration, please configure the following parameters in advance.

**DB Parameter**

| DB Parameter | Value | Description |
| --- | --- | --- |
| LOG_ARCHIVE_FORMAT | - | Set to the same value on all nodes |
| STANDBY_USE_OBSERVER | Y | Required for DR configuration |

**CM Parameter**

| CM Parameter | Value | Description |
| --- | --- | --- |
| _CM_REDIRECT_STDOUT_TO_OUTFILE | Y | Patch FS07PS_341175b required |



---

## Preparing and Placing Deployment Files

### 1. Required File List

- owldb dp binary (`owldb-dp-installer-*.tar.gz`)
- License file (`license.xml`)

{% hint style="info" %}
**Note**

Since Tibero is already installed on the registered DB, the Tibero binary is not required.
{% endhint %}

### 2. File Placement

Navigate to the path where the existing database is installed (hereinafter `설치 디렉터리`). (Example: `/home/rocky/owldb`)

Extract the DP binary at the same level as the existing database's `TB_HOME`.

```bash
# Extract DP binary
tar -zxvf owldb-dp-installer-%Y%m%d-%H.tar.gz -C $TB_HOME --strip-components=2

# Place license file
mv {license file} $TB_HOME/license.xml
```

After preparation, the `$TB_HOME` structure is as follows.

```
$TB_HOME/
 ├── license.xml                      # License file
 └── owldb-dp-installer/
      ├── install/                    # Tibero installation scripts
      ├── validate_infra.sh           # Infrastructure validation script
      ├── install_pkg.sh              # Tibero package installation script
      └── tbagent_dist_latest.tar.gz  # tbagent binary
```

Proceed by navigating to the database server Agent installation documentation.
