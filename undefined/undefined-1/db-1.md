# Installation Guide / Database Server Preparation and Installation / Register DB Environment Preparation Guide

{% hint style="info" %}
**Note**

This guide is intended for customer infrastructure administrators.
{% endhint %}

{% hint style="info" %}
**Note**

To register an existing running Tibero instance with OwlDB for management, it must be **Tibero version 7 or higher**.
{% endhint %}

---

## System Requirements

### Disk (Volume) Requirements

Since the existing database is already configured, no separate preparation is required for Data/Archive/Redo disks. Only the Backup disk needs to be verified.

| Disk | Requirements |
| --- | --- |
| Backup | xfs filesystem creation and mount completed |

{% hint style="info" %}
**Note**

For TAC configurations, the Backup disk must be a shared volume accessible from all nodes.
{% endhint %}

## Network Requirements

### **Required Port Configuration for the Database Server**

The following ports are required to register an existing database with OwlDB.

| Port Type | Port Number | Purpose | Notes |
| --- | --- | --- | --- |
| **DB Listener **<br>**Port** | Existing DB Setting Value | Database connection port<br>Tibero: ex) 8629/tcp | Allow inbound DB Listener port<br>from the OwlDB server |

{% hint style="warning" %}
**Caution**

Do not change ports currently in use by the existing database. Additionally open port 40001 for Agent communication and the Listener port for DB connectivity.
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
| STANDBY_USE_OBSERVER | Y | Required for DR configurations |

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

Since Tibero is already installed on the registration DB, the Tibero binary is not required.
{% endhint %}

### 2. File Placement

Navigate to the path where the existing database is installed (hereafter referred to as `설치 디렉터리`). (Example: `/home/rocky/owldb`)

Extract the DP binary at the same level as the existing database's `TB_HOME`.

```bash
# DP 바이너리 압축 해제
tar -zxvf owldb-dp-installer-%Y%m%d-%H.tar.gz -C $TB_HOME --strip-components=2

# 라이선스 파일 배치
mv {라이선스 파일} $TB_HOME/license.xml
```

After preparation is complete, the `$TB_HOME` structure is as follows.

```
$TB_HOME/
 ├── license.xml                      # 라이선스 파일
 └── owldb-dp-installer/
      ├── install/                    # Tibero 설치 스크립트
      ├── validate_infra.sh           # 인프라 검증 스크립트
      ├── install_pkg.sh              # Tibero 패키지 설치 스크립트
      └── tbagent_dist_latest.tar.gz  # tbagent 바이너리
```

Proceed to the database server Agent installation document to continue.
