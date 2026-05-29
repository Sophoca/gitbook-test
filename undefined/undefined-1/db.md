# Installation Guide / Database Server Preparation and Installation / Install DB Environment Preparation Guide

{% hint style="info" %}
**Notice**

This guide is intended for infrastructure administrators at client organizations.
{% endhint %}

---

## System Requirements

### 1. Hardware Requirements

| Item | Minimum Specification | Notes |
| --- | --- | --- |
| CPU | 2 Cores or more | - |
| Memory | 4GB or more | - |
| Disk | - | 3. Disk (Volume) Requirements Verification |

### 2. Operating System Requirements

| Item | Requirements |
| --- | --- |
| OS | Rocky Linux 9.5 or later |

### 3. Disk (Volume) Requirements

For TAC configurations, the following requirements must be met.

- All disks used in a TAC configuration must be **shared volumes accessible from all DB nodes**.

| Purpose | Requirements |
| --- | --- |
| Data / Archive / Redo | Prepare as a shared volume, raw device, or partitioned path<br>(do not create a file system) |
| Backup | Prepare as a shared volume with a file system path |

{% hint style="warning" %}
**Caution**

Since OwlDB automatically configures the Tibero-dedicated file system (TAS) on the Data/Archive/Redo disks, partitioning or file systems must not be created in advance.
{% endhint %}

### 4. Kernel Parameter Configuration

The following kernel parameters must be configured to run the Tibero database. Configure them via '[Kernel Parameter Configuration](https://docs.tibero.com/tibero/topics/installation/installaion-guide/installation-prerequisites#undefined-4)' in the Tibero 'Installation Guide'.



## Network Requirements

### Required Port Configuration for Database Servers

The following ports are required for a new database installation.

| Port Type | Port Number | Purpose | Notes |
| --- | --- | --- | --- |
| **DB Listener Port** | Example)<br>8629/tcp | Database connection port | Allow inbound 8629 from the OwlDB server |
| **Inter-node Internal Connection Port** | Example)<br>8630~8679/tcp | Inter-node internal communication port for TAC configurations <br>(+50 range based on the DB Listener port) | Allow both inbound and outbound between nodes (required only for TAC and DR configurations) |

{% hint style="warning" %}
**Caution**

**⚠️ Important — DB Listener Port Range Notice**

The database uses a range of **+50 ports**based on the designated DB Listener port for inter-node internal connections.

**Example**: When the DB Listener port is 8629

- DB Listener Port: 8629/tcp
- Inter-node Internal Connection Ports: 8630/tcp ~ 8679/tcp (50 ports total)

Therefore, when configuring the DB Listener port, all ports in the +50 range must be free. No other applications or services may be using that port range, and port conflicts may cause database installation or TAC configuration to fail.
{% endhint %}

### Firewall Configuration

Firewall configuration is required for communication between the OwlDB server and the database server.



---

## Deployment File Preparation and Placement

### 1. Required File List

- owldb dp binary (`owldb-dp-installer-*.tar.gz`)
- tibero binary (`tibero.tar.gz`)
- License file (`license.xml`)

### 2. Creating the Installation Directory

Create the path where the database will be installed (hereinafter referred to as `설치 디렉터리`) (example: `/home/rocky/owldb`)

```bash
mkdir -p {설치 디렉터리}/tibero
chmod 755 {설치 디렉터리}/tibero
```

`{설치 디렉터리}/tibero` This path will be used in subsequent steps `$TB_HOME`is used as.

### **3. File Placement**

Decompress the DP binary to `$TB_HOME`, and place the tibero binary and license file.

```bash
# DP 바이너리 압축 해제
tar -zxvf owldb-dp-installer-%Y%m%d-%H.tar.gz -C $TB_HOME --strip-components=2

# tibero 바이너리 배치
mv {tibero 바이너리 파일} $TB_HOME/tibero.tar.gz

# 라이선스 파일 배치
mv {라이선스 파일} $TB_HOME/license.xml
```

After preparation is complete, `$TB_HOME` the structure is as follows.

```
$TB_HOME/
 ├── tibero.tar.gz                    # tibero 바이너리
 ├── license.xml                      # 라이선스 파일
 └── owldb-dp-installer/
      ├── install/                    # Tibero 설치 스크립트
      ├── validate_infra.sh           # 인프라 검증 스크립트
      ├── install_pkg.sh              # Tibero 패키지 설치 스크립트
      └── tbagent_dist_latest.tar.gz  # tbagent 바이너리
```

After that, [Database Server Agent Installation Documentation](undefined/undefined-1/agent.md)proceed by navigating to.
