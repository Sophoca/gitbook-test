# Feature Usage Guide / Dashboard / Database Installation

Install the database to operate it in OwlDB. Once the database installation is complete, all features provided by OwlDB become available. 

**Verify the following items before installation.**

- The installation feature is available to administrator accounts only.

## Standard Architecture

OwlDB provides a new database installation feature based on the standard architecture. The standard architectures provided by OwlDB On-premise are as follows.

| Configuration | Description |
| --- | --- |
| Single | Single-node configuration |
| TAC | Up to 4-node cluster configuration |
| Single + DR | Single configuration with 1 fixed Standby node |
| TAC + DR | TAC configuration with 1 fixed Standby node |

For TAC and DR configurations, all nodes are configured with identical specs, and the number of Standby nodes is fixed at 1 for DR configurations.

{% hint style="info" %}
**Note**

A Multi-node Cluster cannot be configured as a Standby, and a maximum of 1 Standby node is supported.
{% endhint %}

{% hint style="warning" %}
**Caution**

If the database configuration is changed directly from outside without going through OwlDB, some OwlDB features may not function correctly. If a configuration change is needed, it must be performed through OwlDB.
{% endhint %}

## OwlDB Standard Architecture



---

## **Installation Process**

1. **OwlDB console screen** > **Dashboard**Navigate to.
2. At the top of the dashboard,** [Install]** Click the button to go to the installation page.
3. Enter the installation options step by step. Installation option entry consists of 5 steps in total; for details on each step, refer to the 
[**Installation Option Steps **](#undefined-2)section below.
4. Review the entered information and, once the installation feasibility check is complete, **[Install]** Click the button.
5. Once installation starts, you can check the progress status in the dashboard list. When the status changes to **Running**, the installation has completed successfully.

{% hint style="info" %}
**Reference**

The database installation feature is available only from the Root account.

The database installation page can also be accessed via the following paths.

- OwlDB console screen > Dashboard > Card view > + icon
- GNB > DB Alias dropdown > Database Install button
{% endhint %}

---

## **Installation Option Steps**

{% tabs %}
{% tab title="엔진 옵션" %}
This step configures the database alias, engine, and topology information.

| Item | Description |
| --- | --- |
| Database Alias* | An alias used to identify the database |
| Database Engine Type* | The database engine to use<br>- **Tibero**<br>- **Tmax OpenSQL** (Support planned for a future release) |
| Topology* | The topology type that determines the database structure<br>- **Single**<br>- **TAC** |
| Node Count* | Number of nodes in the cluster configuration |
{% endtab %}
{% tab title="DR 구성" %}
This step configures DR usage and the failover automation level.

| Item | Description | Remarks |
| --- | --- | --- |
| Enable DR* | Whether to use DR configuration | - |
| Failover Automation Level* | [Automatic failover step<br>- Level 0: Manual<br>- Level 1: Automatic failover](#undefined)<br>- Level 0: Manual<br>- Level 1: Automatic failover<br>- Level 2: Automatic configuration recovery (Not supported in OwlDB v1.3) <br>- Level 3: Full automation | - |
| Standby Count* | Number of Standby DBs | The maximum number of Standby DBs supported in the current standard architecture is 1 |
| Standby Mode* | Standby Mode Options<br>- **Recovery**<br>- **Read Only** | - |
| Log Replication Type | Log transfer method from Primary to Standby<br>• **LGWR ASYNC : **A replication mode that transmits Redo logs generated in real time as transactions occur<br>• **ARCH ASYNC : **A replication mode that collects and transmits archive log files after a log switch occurs and the files are created | - |

{% hint style="info" %}
When DR usage is selected in the Enable DR item **Failover Automation Level, Standby Count, Standby Mode, Log Replication Type** items are displayed.

The supported level of Failover Automation Level varies depending on the topology.

- Single : **Levels 0, 1, 3 **/ TAC : **Levels 0, 1**

When using ARCH ASYNC mode, synchronization to Standby may be delayed depending on the interval at which archive logs are generated (up to approximately 10 minutes).
{% endhint %}
{% endtab %}
{% tab title="인스턴스 구성" %}
Input items per node are automatically configured according to the topology. ****notation indicates a required input field.&nbsp;&nbsp;&nbsp;&nbsp;*

### Single

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | In accordance with the selected topology configuration,<br>select the host on which to install the database | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the port to be used for communication between OwlDB and the database server | If using port forwarding, <br>enter the external port |
| Data Path* | Enter the Data Path | Only file system paths can be entered |
| Redo Path* | Enter the Redo Path | Only file system paths can be entered |
| Archive Path* | Enter the Archive Path | Only file system paths can be entered |
| Backup Path* | Enter the Backup Path | Only file system paths can be entered |

**Each Path**only accepts file system paths. Entering the same path or duplicate different paths is also permitted.

However, the following conditions must be met:

- The entered path must **actually exist**on the target installation host.
- The DP Agent execution account must have **read, write, and execute permissions**on the file system path.



---

### Single+DR

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | In accordance with the selected topology configuration,<br>select the host on which to install the database | - |
| Service IP* | Enter or select the IP to be used for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Enter the port to be used for communication between OwlDB and the database server | If using port forwarding, enter the external port |
| Primary Destination IP*(Enter for Primary instance only) | Enter the Primary Destination IP to be used for communication from StandByDB to PrimaryDB | If using NAT, enter the NAT IP<br>Enter for Primary instance only |
| Primary Destination Port*<br>(Enter for Primary instance only) | Enter the Primary Destination Port to be used for communication from StandBy DB to Primary DB | If using port forwarding, enter the external port |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Enter the StandBy Destination IP to be used for communication from Primary DB to StandBy DB | If using NAT, enter the NAT IP |
| StandBy Destination Port*<br>(Enter for StandBy instance only) | Enter the StandBy Destination Port to be used for communication from Primary DB to StandBy DB | If using port forwarding, enter the external port |
| Data Path* | Enter Data Path | Only file system paths can be entered |
| Redo Path* | Enter Redo Path | Only file system paths can be entered |
| Archive Path* | Enter Archive Path | Only file system paths can be entered |
| Backup Path* | Enter Backup Path | Only file system paths can be entered |
| SSH Port* | SSH port | - |
| SSH User* | SSH User | - |
| SSH Key File Path* | Enter the private key path to be used for SSH access between instances | Enter a common private key path so that the same private key is used for SSH access between instances |

{% hint style="info" %}
**Note**

If using a DR configuration, the SSH Key File must be placed in the designated path in advance. For detailed configuration instructions, refer to [SSH Public Key Setup Between Nodes](#4VCx1BdX0fpROq6CwGnH)for details.
{% endhint %}

**All Path**fields only accept file system paths. Entering the same path or duplicate different paths is also permitted.

However, the following conditions must be met:

- The entered path must **actually exist**on the target installation host.
- The DP Agent execution account must have **read, write, and execute permissions**on the file system path.



---

### TAC

| Item | Item | Remarks |
| --- | --- | --- |
| Hostname* | According to the selected topology configuration,<br>select the host on which to install the database | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If using port forwarding, enter the external Port |
| Interconnect IP* | Select the Interconnect IP to be used for communication between nodes within the Cluster from the list | Enter for both Primary and StandBy clusters |
| Data Path* | Enter the Data Path | Enter a raw device or partition path; shared volume is used |
| Redo Path* | Enter the Redo Path | Enter a raw device or partition path; shared volume is used |
| Archive Path* | Enter the Archive Path | Enter a raw device or partition path; shared volume is used |
| Backup Path* | Enter the Backup Path | Only a file system path can be entered |

**Data Path, Redo Path, Archive Path**accepts a raw device path (`/dev/sdb`) or a partition path (`/dev/sdb1`). 
**Backup Path**only accepts a file system path. 

However, the following conditions must be met:

- All entered paths must be **shared volumes**.
- The entered path must **actually exist**on the target installation host.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### TAC+DR

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | In accordance with the selected topology configuration,<br>select the host on which to install the database | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node. | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If using port forwarding, enter the external Port |
| Interconnect IP* | Select the Interconnect IP to be used for communication between nodes within the Cluster from the list | Enter for both Primary and StandBy clusters |
| Primary Destination IP*(Enter for Primary instance only) | Directly enter the Primary Destination IP to be used for communication from the StandBy DB to the Primary DB | If using NAT, enter the NAT IP |
| Primary Destination Port*<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to be used for communication from the StandBy DB to the Primary DB | If using port forwarding, enter the external Port |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to be used for communication from the Primary DB to the StandBy DB | If using NAT, enter the NAT IP |
| StandBy Destination Port*<br>(StandBy instance input only) | Enter the StandBy Destination Port to be used for communication from the Primary DB to the StandBy DB | If port forwarding is used, enter the external port |
| Data Path* | Enter the data path | Enter a raw device or partition path; shared volume must be used |
| Redo Path* | Enter the Redo Path | Enter a raw device or partition path; shared volume must be used |
| Archive Path* | Enter the Archive Path | Enter a raw device or partition path; shared volume must be used |
| Backup Path* | Enter the Backup Path | Only file system paths can be entered |
| SSH Port* | SSH port | - |
| SSH User* | SSH User | - |
| SSH Key File Path* | Enter the private key path to be used for SSH connections between instances | Enter a common private key path so that the same private key is used for SSH connections between instances |

{% hint style="info" %}
**Note**

When using a DR configuration, the SSH Key File must be placed at the designated path in advance. For detailed configuration instructions, refer to [SSH Public Key Setup Between Nodes](#4VCx1BdX0fpROq6CwGnH)for details.
{% endhint %}

**Data Path, Redo Path, Archive Path**accepts a raw device path (`/dev/sdb`) or a partition path (`/dev/sdb1`). 
**Backup Path**only accepts file system paths. 

However, the following conditions must be met:

- All entered paths must be configured as **shared volumes**.
- The entered path must **actually exist**on the target installation host.
- The DP Agent execution account must have **read, write, and execute permissions**on the file system path.

{% hint style="info" %}
**Note**

The input fields above are automatically configured for the number of nodes required based on the selected topology. 

For a stable operating environment, all instances in the cluster are automatically configured with identical specifications.
{% endhint %}
{% endtab %}
{% tab title="데이터베이스 구성" %}
This is the step for entering database configuration information.

| Item | Description |
| --- | --- |
| Database Name* | Name of the database to use |
| SYS User Password* | Password for the highest-privilege database administrator account (SYS user) |
| Target Memory Size* | Target memory size |
| Shared Memory Size* | Shared memory size |
| Character Set* | Character encoding to use for the database |
| Timezone* | OS timezone where the database will be installed |
| VIP* | Select whether to use VIP |
| Primary Node #N Vip | Database virtual IP<br>(Activated when VIP usage is selected) |
| Database Listener Port | Database listener port for network communication |
| Max Session Count | Maximum number of concurrently allowed sessions |
| Redo Log File Size (MB) | Redo log file size |
| System Data File Size (MB) | Size of the data file for storing system tables and key metadata |
| Syssub Data File Size (MB) | Sub data file size for storing system operation-related data |
| User Tablespace Data File Size (MB) | Tablespace data file size for storing user data |
| Temporary Tablespace Data File Size (MB) | Temporary tablespace data file size used for large-volume operations |
| Undo Tablespace Data File Size (MB) | Undo tablespace size |
{% endtab %}
{% tab title="구성 정보 확인" %}
You can proceed to this step only after all options entered in the previous steps have been validated.

Review all entered configuration information at a glance, and if everything looks correct, click the **[Install]** button to begin installation.
To make changes, click the **[Previous]** button.
{% endtab %}
{% endtabs %}







---

## Installation Progress

You can monitor the database installation progress in real time from the dashboard. Installation proceeds through major phases and sub-phases as shown in the table below; the actual steps performed may vary depending on the selected topology.

| Major Phase | Sub-phase |
| --- | --- |
| Installation prerequisite validation | 1. sudo privilege validation<br>2. Required file validation<br>3. parameter config validation |
| Infrastructure Setup | 1. Kernel environment configuration<br>2. Required package installation<br>3. Disk udev rule configuration<br>4. Volume mount<br>5. Disk attach (instance) |
| Tibero Configuration | 1. Tibero instance Tip file & DSN file creation<br>2. Volume configuration change due to sequential cm installation<br>3. Volume wait due to sequential cm installation<br>4. Tip convert (primary <→ standby)<br>5. Standby installation complete tag configuration change<br>6. Standby installation complete tag wait<br>7. RMGR backup and transfer<br>8. RMGR backup wait |
| DB Installation | 1. CM gen (resource registration and execution)<br>2. DB create (including TAS depending on topology)<br>3. Disk snapshot creation<br>4. wait Disk snapshot in Standby node<br>5. CM Fence on (reboot)<br>6. cm complete (service up)<br>7. wait cm service<br>8. recovery RMGR |
| Tibero Status Check | 1. Tb probe |
