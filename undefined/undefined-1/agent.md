# Installation Guide / Database Server Preparation and Installation / Database Server Agent Installation

{% hint style="info" %}
**Note**

This guide should be followed after completing the [Installation DB Environment Preparation Guide](undefined/undefined-1/db.md) or [Registration DB Environment Preparation Guide](undefined/undefined-1/db-1.md).
{% endhint %}

## Running the Infrastructure Validation Script

Validates that the infrastructure is correctly configured before installing the Agent.

```bash
cd $TB_HOME
sh validate_infra.sh --mode DP
```

The validation items are as follows.

- CPU and Memory size
- Disk size
- Whether the Tibero package is installed
- Network connectivity status
- Firewall port configuration
- Required file list

{% hint style="warning" %}
**Caution**

If any items fail validation, remediation must be completed and re-validation must be performed. Proceed with package installation and Agent installation only after all items have passed.
{% endhint %}

## Package Installation

Install packages after passing all infrastructure validation checks.

{% tabs %}
{% tab title="외부 인터넷 연결이 가능한 경우" %}
```bash
cd $TB_HOME
sudo bash install_pkg.sh
```
{% endtab %}
{% tab title="인터넷 연결이 불가한 경우" %}
Manually pre-install the following packages.

- Tibero package: Refer to the Tibero package installation guide
- OwlDB package: `openssh-server`, `openssh-clients`, `sshpass`, `udev`, `xfsprogs`, `iproute`
{% endtab %}
{% endtabs %}

## Agent Installation and Startup

### 1. Extract the Agent binary archive

```bash
tar -zxvf $TB_HOME/tbagent_dist_latest.tar.gz -C $TB_HOME
```

### **2. Write the agent.env file**

Enter the information required to start the agent into the env file.

```
##########################################################
#                    AGENT ENV FILE                      #
#--------------------------------------------------------#
# This file contains environment variables for the agent #
# Do NOT add spaces around '='                          #
# Lines starting with '#' are comments                  #
##########################################################

# Network Configuration (OwlDB)
IP=
PORT=

# User Configuration
USERNAME=

# Tibero Configuration
TB_HOME=

# Only Register Variables [OPTIONAL]
TB_SID=
TAS_SID=
CM_SID=
CM_HOME=
```

Whether each parameter is required depends on the configuration method.

{% tabs %}
{% tab title="설치 DB" %}
| Option | Description | Required |
| --- | --- | --- |
| `IP` | OwlDB server IP address | Required |
| `PORT` | OwlDB server port (SERVER_PORT) | Required |
| `USERNAME` | DB OS username | Required |
| `TB_HOME` | Tibero home directory path | Required |
| `TB_SID` | TB_SID value | Not required during installation |
| `TAS_SID` | TAS_SID value | Not required during installation |
| `CM_SID` | CM_SID value | Not required during installation |
| `CM_HOME` | CM_HOME value | Not required during installation |

{% hint style="info" %}
**Note**

`TB_SID` DB identification values such as these are set automatically by OwlDB during the installation process. They do not need to be entered at the pre-installation stage.
{% endhint %}
{% endtab %}
{% tab title="등록 DB" %}
| Option | Description | Required |
| --- | --- | --- |
| `IP` | OwlDB server IP address | Required |
| `PORT` | OwlDB server port (SERVER_PORT) | Required |
| `USERNAME` | OS username under which Tibero was installed | Required |
| `TB_HOME` | Tibero home directory path | Required |
| `TB_SID` | TB_SID value | **Required** |
| `TAS_SID` | TAS_SID value | Required for TAC configuration; not required if unused |
| `CM_SID` | CM_SID value | Required for CM configuration; not required if unused |
| `CM_HOME` | CM_HOME value | Required for CM configuration; not required if unused |

{% hint style="warning" %}
**Caution**

Since a registration DB targets an existing database already in operation, `TB_SID`must be set to the SID value of the existing Tibero instance.
{% endhint %}
{% endtab %}
{% endtabs %}

### 3. Run the Agent installation script

```bash
cd $TB_HOME/tbagent_dist
sh tbagent_start.sh
```

{% hint style="info" %}
**Caution**

`tbagent_start.sh` The script registers the Agent as a systemd service and timer, and sudo privileges are used during this process.

When restarting the Agent [Reference > Precautions When Restarting the Agent](references/agent.md)must be verified.
{% endhint %}

### 4. OS user sudoers configuration

Some commands are executed with sudo during database installation and operation. If a password prompt appears during script execution, the process may be interrupted, so configure NOPASSWD for the OS user used for installation.

```bash
# 1. sudoers 설정 파일 생성
sudo tee /etc/sudoers.d/{username} << 'EOF'
{username} ALL=(ALL) NOPASSWD: \
        /usr/bin/systemctl \
        /usr/bin/timedatectl \
        /usr/sbin/udevadm \
        /usr/bin/dd \
        /usr/bin/tar \
        /usr/bin/mkdir \
        /usr/bin/rm \
        /usr/bin/unlink \
        /usr/bin/ln \
        /usr/bin/chown \
        /usr/bin/chmod \
        /usr/bin/tee \
        /usr/bin/sed \
        /usr/bin/bash \
        /usr/bin/su \
        /usr/lib/udev/scsi_id \
        /usr/bin/grep \
        /usr/bin/touch \
        /usr/bin/kill \
    )
EOF

# 2. 파일 권한 설정
sudo chmod 440 /etc/sudoers.d/{username}

# 3. 적용 확인
sudo -l -U {username}
```
