# Feature Usage Guide / Dashboard / Database Exploration / Database Registration

You can register and manage already-running databases in OwlDB. Registration is supported not only for databases built on standard architectures, but also for databases with non-standard architectures configured directly by customers.

Once registration is complete, you can use features provided by OwlDB such as monitoring and parameter management. 



**Verify the following items before registration.**

- The registration feature is available only to administrator accounts.
- The boot mode of the DB node to be registered must be `Normal`, `Recovery`, `Readonly` . Nodes started with any other boot mode will be treated as abnormal nodes.
- Standby multi-node configurations are not supported for registration.



## Registration Process

1. OwlDB console screen > Dashboard > **[Discover]** Click the button.
2. In the discovery results, **Registerable DB** check the list, and click the **[Register]** button for the target database to navigate to the registration page.
3. Enter the registration options step by step. Registration option input consists of 5 steps in total, and for details on each step, refer to the '**Registration Option Steps'**section below.
4. Review the entered information and click the **[Register]** button.
5. When the status of the database in the dashboard list is displayed as **Running**, registration has been completed successfully.

---

## **Registration Option Steps**

When you navigate to the registration page, the database information collected through discovery is automatically populated. Automatically populated fields cannot be changed; only certain fields that could not be collected require manual input.

{% tabs %}
{% tab title="엔진 옵션" %}
This step configures the database alias, engine, and topology information.

| Item | Description |
| --- | --- |
| Database Alias* | An alias used to identify the database |
| Database Engine Type | The database engine to use **Tibero**<br>- **Tmax OpenSQL** (to be supported in a future release) |
| Topology | The topology type that determines the database structure **Single**<br>- **TAC** |
| Node Count | The number of nodes in the cluster configuration |
{% endtab %}
{% tab title="DR 구성" %}
This step configures whether to use DR and the failover automation level.

| Item | Description | Remarks |
| --- | --- | --- |
| Enable DR | Whether to use DR configuration | - |
| Failover Automation Level* | [Automatic failover level](#undefined)<br>- **Level 0: Manual**<br>- **Level 1: Automatic Failover**<br>- **Level 2: Automatic Configuration Recovery** **(not supported in OwlDB v1.3) **<br>- **Level 3: Full Automation** | - |
| Standby Count | The number of Standby DBs | - |
| Standby Mode | Standby Mode options **Recovery**<br>- **Read Only** | - |
| Log Replication Type | The log transmission method from Primary to Standby<br>• **LGWR ASYNC: **A replication mode that transmits Redo logs generated in real time when a transaction occurs<br>• **ARCH ASYNC: **A replication mode that collects and transmits archive log files once they are created after a log switch | - |

{% hint style="info" %}
**Note**

When DR is selected in the Enable DR item **Failover Automation Level, Standby Count, Standby Mode, Log Replication Type** items are displayed.

The supported levels of Failover Automation Level differ depending on the topology.

- Single : **Levels 0, 1, 3 **/ TAC : **Levels 0, 1**

When using ARCH ASYNC mode, synchronization to Standby may be delayed depending on the interval at which archive logs are generated (up to approximately 10 minutes).
{% endhint %}
{% endtab %}
{% tab title="인스턴스 구성" %}
Input items per node are automatically configured depending on the topology. ****notation indicates a required input field.&nbsp;&nbsp;&nbsp;&nbsp;*

### Single

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If using port forwarding, <br>enter the external Port |
| Backup Path* | Enter the Backup Path | Only file system paths can be entered |

**Path**only accepts file system paths. 

However, the following conditions must be met.

- The entered path must **actually exist**on the target host to be registered.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### Single+DR

| Item | Description | Notes |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If using port forwarding, enter the external Port |
| Primary Destination IP*(Enter for Primary instance only) | Directly enter the Primary Destination IP to be used for communication from StandByDB to PrimaryDB | If using NAT, enter the NAT IP<br>Enter for Primary instance only |
| Primary Destination Port*<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to be used for communication from StandBy DB to Primary DB | If using port forwarding, enter the external Port |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to be used for communication from Primary DB to StandBy DB | If using NAT, enter the NAT IP |
| StandBy Destination Port*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination Port to be used for communication from Primary DB to StandBy DB | If using port forwarding, enter the external Port |
| Backup Path* | Enter Backup Path | Only file system paths can be entered |

**Path**only accepts file system paths. 

However, the following conditions must be met.

- The entered path must **actually exist**on the target host to be registered.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### TAC

| Item | Item | Notes |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to use for communication between OwlDB and the node | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to use for communication between OwlDB and the database server | If using port forwarding, enter the external Port |
| Backup Path* | Enter Backup Path | Only file system paths can be entered,<br>shared volume required |

**Backup Path**only accepts file system paths. 

However, the following conditions must be met.

- All entered paths must be **shared volumes**.
- The entered path must **actually exist**on the target host to be installed.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### TAC+DR

| Item | Description | Note |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to use for communication between OwlDB and the node. | If using NAT, enter the NAT IP |
| Service Port* | Directly enter the Port to use for communication between OwlDB and the database server | If using port forwarding, enter the external Port |
| Primary Destination IP*(Enter for Primary instance only) | Directly enter the Primary Destination IP to use for communication from StandBy DB to Primary DB | If using NAT, enter the NAT IP |
| Primary Destination Port*<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to use for communication from StandBy DB to Primary DB | If using port forwarding, enter the external Port |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to use for communication from Primary DB to StandBy DB | If using NAT, enter the NAT IP |
| StandBy Destination Port*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination Port to use for communication from Primary DB to StandBy DB | Enter the external port when using port forwarding |
| Backup Path* | Enter Backup Path | Only file system paths can be entered,<br>use shared volumes |

**Backup Path**only accepts file system paths. 

However, the following conditions must be met.

- All entered paths must be configured as **shared volumes**.
- The entered path must **actually exist**on the target installation host.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.
{% endtab %}
{% tab title="데이터베이스 구성" %}
This step involves verifying the database configuration information and manually entering certain items that cannot be collected automatically.

| Item | Description |
| --- | --- |
| Database Name | The name of the database to use |
| SYS User Password* | The password for the highest-privilege database administrator account (SYS user) |
| Character Set | The character encoding to use for the database |
| Timezone | The OS timezone where the database will be installed |
| VIP | The virtual IP of the database |
| Database Listener Port | The database listener port for network communication |
| Max Session Count | The maximum number of concurrent sessions allowed |
| Target Memory Ratio | The ratio of target memory |
| Shared Memory Ratio | The ratio of shared memory |
| Redo Log File Size (MB) | The size of the Redo log file |
| System Data File Size (MB) | The size of the data file for storing system tables and key metadata |
| Syssub Data File Size (MB) | The size of the sub data file for storing system operation-related data |
| User Tablespace Data File Size (MB) | The size of the tablespace data file for storing user data |
| Temporary Tablespace Data File Size (MB) | The size of the temporary tablespace data file used for large-scale operations |
| Undo Tablespace Data File Size (MB) | The size of the Undo tablespace |
{% endtab %}
{% tab title="구성 정보 확인" %}
You can proceed to this step only after all options entered in the previous steps have been validated successfully.

Review all entered configuration information at a glance, and if everything looks correct, click the **[Create]** button to begin registration.
To make changes, click the **[Previous]** button.
{% endtab %}
{% endtabs %}

****indicates a required field. All other fields are pre-populated with information collected through discovery.*

---

## Deregistration

A registered database can be removed from OwlDB management through deregistration rather than deletion. Even after deregistration, the actual database remains intact in the operational environment and can be re-registered if needed.

Deregistration can be performed from the following locations.

- **Overview** > Actions > **[Deregister]** Click
- **Dashboard** > Select Database > **[Deregister]** Click

**[Deregister]** Clicking the button displays a confirmation modal. Enter the Database Alias and click the **[Confirm]** button to complete the deregistration.
