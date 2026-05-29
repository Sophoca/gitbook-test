# Database Registration

You can register and manage databases that are already in operation in OwlDB. Registration is supported not only for databases built on standard architectures, but also for databases with non-standard architectures configured directly by the customer.

Once registration is complete, you can use features provided by OwlDB such as monitoring and parameter management. 



**Verify the following before registration.**

- The registration feature is available only to administrator accounts.
- The boot mode of the DB node to be registered must be `Normal`, `Recovery`, `Readonly` . Nodes started in any other boot mode are treated as abnormal nodes.
- Standby multi-node configurations are not supported for registration.



## Registration Process

1. OwlDB console screen > Dashboard > **[Discover]** Click the button.
2. In the discovery results, check the **Registerable DBs** list, and click the **[Register]** button for the corresponding database to navigate to the registration page.
3. Enter the registration options step by step. Registration option input consists of a total of 5 steps; for details on each step, refer to the '**Registration Option Steps'**section below.
4. Review the entered information and click the **[Register]** button.
5. When the status of the corresponding database in the dashboard list is displayed as **Running**, registration has been completed successfully.

---

## **Registration Option Steps**

When you navigate to the registration page, database information collected through discovery is automatically populated. Automatically populated fields cannot be modified; only certain fields that could not be collected require manual input.

{% tabs %}
{% tab title="Engine Options" %}
This step configures the database alias, engine, and topology information.

| Field | Description |
| --- | --- |
| Database Alias* | An alias used to identify the database |
| Database Engine Type | The database engine to use<br>- **Tibero**<br>- **Tmax OpenSQL** (planned for future support) |
| Topology | The topology type that determines the database structure<br>- **Single**<br>- **TAC** |
| Node Count | Number of nodes in the cluster configuration |
{% endtab %}
{% tab title="DR Configuration" %}
This step configures whether DR is enabled and the failover automation level.

| Item | Description | Remarks |
| --- | --- | --- |
| Enable DR | Whether to use DR configuration | - |
| Failover Automation Level* | [Automatic failover step<br>-](#undefined)<br>- **Level 0: Manual**<br>- **Level 1: Automatic Failover**<br>- **Level 2: Automatic Configuration Recovery** **(not supported in OwlDB v1.3) **<br>- **Level 3: Full Automation** | - |
| Standby Count | Number of Standby DBs | - |
| Standby Mode | Standby Mode options<br>- **Recovery**<br>- **Read Only** | - |
| Log Replication Type | The log transfer method from Primary to Standby<br>• **LGWR ASYNC: **A replication mode that transmits Redo logs generated in real time when a transaction occurs<br>• **ARCH ASYNC: **Replication mode in which archive log files are collected and transmitted after a log switch occurs and the archive log file is generated | - |

{% hint style="info" %}
**Note**

When DR usage is selected in the Enable DR item **Failover Automation Level, Standby Count, Standby Mode, Log Replication Type** items are displayed.

The supported level of Failover Automation Level varies depending on the topology.

- Single : **Levels 0, 1, 3 **/ TAC : **Levels 0, 1**

When using ARCH ASYNC mode, synchronization to Standby may be delayed depending on the interval at which archive logs are generated (up to approximately 10 minutes).
{% endhint %}
{% endtab %}
{% tab title="Instance Configuration" %}
Input items per node are automatically configured according to the topology. ****notation indicates a required input field.&nbsp;&nbsp;&nbsp;&nbsp;*

### Single

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to use for communication between OwlDB and the node | Enter the NAT IP if using NAT |
| Service Port* | Directly enter the Port to use for communication between OwlDB and the database server | If using port forwarding, <br>enter the external Port |
| Backup Path* | Enter the Backup Path | Only file system paths can be entered |

**Path**only accepts file system paths. 

However, the following conditions must be met:

- The entered path must **actually exist**on the target host to be registered.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### Single+DR

| Item | Description | Notes |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to use for communication between OwlDB and the node | Enter the NAT IP if using NAT |
| Service Port* | Directly enter the Port to use for communication between OwlDB and the database server | Enter the external Port if using port forwarding |
| Primary Destination IP*(Enter for Primary instance only) | Directly enter the Primary Destination IP to use for communication from StandByDB to PrimaryDB | Enter the NAT IP if using NAT<br>Enter for Primary instance only |
| Primary Destination Port*<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to use for communication from StandBy DB to Primary DB | Enter the external Port if using port forwarding |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to use for communication from Primary DB to StandBy DB | Enter the NAT IP if using NAT |
| StandBy Destination Port*<br>(Enter for StandBy instance only) | Enter the StandBy Destination Port to be used for communication from Primary DB to StandBy DB | If port forwarding is used, enter the external Port |
| Backup Path* | Enter Backup Path | Only file system paths can be entered |

**Path**only accepts file system paths. 

However, the following conditions must be met:

- The entered path must **actually exist**on the target host to be registered.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### TAC

| Item | Item | Notes |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node | If NAT is used, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If port forwarding is used, enter the external Port |
| Backup Path* | Enter Backup Path | Only file system paths can be entered,<br>shared volume required |

**Backup Path**only accepts file system paths. 

However, the following conditions must be met:

- All entered paths must be **shared volumes**.
- The entered path must **actually exist**on the target host to be installed.
- The DP Agent execution account must have **read, write, and execute permissions**for the file system path.



---

### TAC+DR

| Item | Description | Remarks |
| --- | --- | --- |
| Hostname* | Select the host to map to the DB node | - |
| Service IP* | Directly enter or select the IP to be used for communication between OwlDB and the node. | If NAT is used, enter the NAT IP |
| Service Port* | Directly enter the Port to be used for communication between OwlDB and the database server | If port forwarding is used, enter the external Port |
| Primary Destination IP*(Enter for Primary instance only) | Directly enter the Primary Destination IP to be used for communication from StandBy DB to Primary DB | If NAT is used, enter the NAT IP |
| Primary Destination Port*<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to be used for communication from StandBy DB to Primary DB | If port forwarding is used, enter the external Port |
| StandBy Destination IP*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to be used for communication from Primary DB to StandBy DB | If using NAT, enter the NAT IP |
| StandBy Destination Port*<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination Port to be used for communication from the Primary DB to the StandBy DB | If using port forwarding, enter the external port |
| Backup Path* | Enter the Backup Path | Only file system paths can be entered,<br>use a shared volume |

**Backup Path**only accepts file system paths. 

However, the following conditions must be met:

- All entered paths must be **shared volumes**configured as such.
- The entered path must **actually exist**on the target installation host.
- The account running the DP Agent must have **read, write, and execute permissions**on the file system path.
{% endtab %}
{% tab title="Database Configuration" %}
This is the step where you review the database configuration information and manually enter certain items that cannot be collected automatically.

| Item | Description |
| --- | --- |
| Database Name | The name of the database to use |
| SYS User Password* | The password for the highest-privilege database administrator account (SYS user) |
| Character Set | The character encoding to use for the database |
| Timezone | The OS timezone where the database will be installed |
| VIP | The virtual IP of the database |
| Database Listener Port | The database listener port for network communication |
| Max Session Count | The maximum number of concurrent sessions allowed |
| Target Memory Ratio | The target memory ratio |
| Shared Memory Ratio | The shared memory ratio |
| Redo Log File Size (MB) | The size of the Redo log file |
| System Data File Size (MB) | The size of the data file for storing system tables and key metadata |
| Syssub Data File Size (MB) | The size of the sub data file for storing system operation-related data |
| User Tablespace Data File Size (MB) | The size of the tablespace data file for storing user data |
| Temporary Tablespace Data File Size (MB) | The size of the temporary tablespace data file used for large-scale operations |
| Undo Tablespace Data File Size (MB) | The size of the Undo tablespace |
{% endtab %}
{% tab title="Configuration Review" %}
You can proceed to this step only after all options entered in the previous steps have been validated successfully.

Review all entered configuration information at a glance, and if everything looks correct, **[Create]** click the button to begin registration.
To make changes, **[Previous]** click the button.
{% endtab %}
{% endtabs %}

****indicates a required field. All other fields are pre-populated with information collected through discovery.*

---

## Deregistration

A registered database can be removed from OwlDB management not by deletion, but by deregistration. Even after deregistration, the actual database remains intact in the operating environment and can be re-registered if needed.

Deregistration can be performed from the following locations:

- **Overview** > Actions > **[Deregister]** Click
- **Dashboard** > Select Database > **[Deregister]** Click

**[Deregister]** Clicking the button displays a confirmation modal; enter the Database Alias and **[OK]** Clicking the button completes the deregistration.
