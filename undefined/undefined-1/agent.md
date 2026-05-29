# Database Server Agent Installation

{% hint style="info" %}
**Note**

This guide should be followed after completing the [Installation DB Environment Preparation Guide](db.md) or [Registration DB Environment Preparation Guide](db-1.md).
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

Install the package after passing all infrastructure validation checks.

{% tabs %}
{% tab title="If external internet access is available" %}
```bash
cd $TB_HOME
sudo bash install_pkg.sh
```
{% endtab %}
{% tab title="If internet access is not available" %}
Manually install the following packages in advance.

- Tibero package: Refer to the Tibero package installation guide
- OwlDB package: `openssh-server`, `openssh-clients`, `sshpass`, `udev`, `xfsprogs`, `iproute`
{% endtab %}
{% endtabs %}

## Agent Installation and Startup

### 1. Extract the Agent binary archive

```bash
tar -zxvf $TB_HOME/tbagent_dist_latest.tar.gz -C $TB_HOME
```

### **2. Configure the agent.env file**

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

Whether each parameter is required varies depending on the configuration method.

{% tabs %}
{% tab title="Installation DB" %}
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
{% tab title="Registration DB" %}
| Option | Description | Required |
| --- | --- | --- |
| `IP` | OwlDB server IP address | Required |
| `PORT` | OwlDB server port (SERVER_PORT) | Required |
| `USERNAME` | OS username of the user who installed Tibero | Required |
| `TB_HOME` | Tibero home directory path | Required |
| `TB_SID` | TB_SID value | **Required** |
| `TAS_SID` | TAS_SID value | Required for TAC configuration; not required if not used |
| `CM_SID` | CM_SID value | Required for CM configuration; not required if not used |
| `CM_HOME` | CM_HOME value | Required for CM configuration; not required if not used |

{% hint style="warning" %}
**Caution**

Because a Registration DB targets an existing operational database, `TB_SID`must be set to the SID value of the existing Tibero instance.
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

When restarting the Agent [Reference > Precautions When Restarting the Agent](../../references/agent.md)must be checked without fail.
{% endhint %}

### 4. OS user sudoers Configuration

Some commands are executed with sudo during database installation and operation. If a password prompt occurs during script execution, the task may be interrupted, so configure NOPASSWD for the OS user to be used for installation.

```bash
# 1. Create sudoers configuration file
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

# 2. Set file permissions
sudo chmod 440 /etc/sudoers.d/{username}

# 3. Verify application
sudo -l -U {username}
```
