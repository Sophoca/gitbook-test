# Spec Change

This feature allows you to change the configuration of a running database. Spec changes are possible when the database operational status is `Running` or `Degraded`.

## How to Change Specs

The spec change page can be accessed in the following two ways.

1. **Accessing Spec Change from Overview** Overview page > Actions > Click the Spec Change button
2. **Accessing Spec Change from Change-Detected DB** Dashboard > Explore > Change-Detected DB > Click the Spec Change button



## **Accessing Spec Change from Overview**

When entering the spec change page via the Actions menu on the Overview page, you can perform the following two operations.

### 1. DB Node Configuration Change

**For installed DBs**, Scale In/Out of Primary nodes is supported within the topology scope of the standard architecture.
For example, in a TAC configuration, the number of Primary nodes can be adjusted from a minimum of 2 to a maximum of 4.

If Scale Out is performed, and the DB is using a VIP, you must enter the VIP for the added nodes in the **Database Configuration** step on the spec change page.

**For registered DBs**, Scale In/Out is not supported.

{% hint style="info" %}
**Note**

Changing the topology itself (e.g., Single → TAC) is not supported in spec change.

If Scale Out is performed on a DB using a VIP, you must enter the VIP for the added nodes in Step 4, Database Configuration.
{% endhint %}

### 2. DR Modification

**For installed DBs**, you can toggle DR between enabled and disabled, and also change the failover automation level. If DR is in use, you can also change the Open Mode and Log Replication Type of Standby nodes. 

**Registered DBs**do not support changing DR enablement. If DR is in use, only the failover automation level and Standby node settings can be changed.

{% hint style="info" %}
**Note**

For supported failover automation levels, refer to the [**Failover Automation documentation**](../../../../references/failover-automation.md).
{% endhint %}



## **Spec Change Steps**

{% tabs %}
{% tab title="Engine Options" %}
This step configures the database alias, engine, and topology information.

| Item | Description | Note |
| --- | --- | --- |
| Database Alias | An alias used to identify the database | Not editable |
| Database Engine Type | The database engine to use<br>- **Tibero**<br>- **Tmax OpenSQL** (planned for future support) | Not editable |
| Topology | The topology type that determines the database structure<br>- **Single**<br>- **TAC** | Not editable |
| Node Count | Number of nodes in the cluster configuration | Not editable |
| Scale In/Out | Primary node list | Available only for installed DBs <br>This list is available |

For installed TAC topology DBs, a **Scale In/Out** item is additionally displayed below Node Count.
You can view the currently configured Primary node list and add or remove nodes.

- **Add** : Clicking the Add button allows you to select an instance from the list of installable hosts.
The selected host is added to the Scale In/Out table and becomes a Scale Out target.
- **Delete** : Select the node to remove from the table, then click the Delete button. The selected node becomes a Scale In target and is shown dimmed in the table.
- **Reset** : Reverts any added or deleted changes back to the initial state.
{% endtab %}
{% tab title="DR Configuration" %}
This step configures whether DR is enabled and the failover automation level.

| Item | Description | Notes |
| --- | --- | --- |
| Enable DR | Whether to use DR configuration | Can only be changed for installed DBs |
| Failover Automation Level | [Automatic failover stage](#undefined)<br>- Level 0: Manual<br>- Level 1: Automatic Failover<br>- Level 2: Automatic Configuration Recovery (Not supported in OwlDB v1.3) <br>- Level 3: Full Automation | Modifiable |
| Standby Count | Number of Standby DBs | The maximum number of Standby DBs supported in the current standard architecture is 1. |
| Standby Scale In/Out | StandBy Node List | Available when DR is in use |
| Standby Mode | Select the Open Mode option for the StandBy node in the StandBy node list<br>- **Recovery**<br>- **Read Only** | - |
| Log Replication Type | Select the log transfer method for the StandBy node in the StandBy node list<br>• **LGWR ASYNC: **A replication mode that transmits Redo logs generated in real time when a transaction occurs<br>• **ARCH ASYNC: **A replication mode that collects and transmits archive log files after a log switch occurs | - |

This step allows you to change DR usage, failover automation level, and Standby node settings.

**DR Usage** (Can only be changed on installed DBs)

| Change Direction | Behavior |
| --- | --- |
| Disabled → Enabled | Proceeds with new Standby node provisioning; failover automation level defaults to Level 1 |
| Enabled → Disabled | Proceeds with Standby node cleanup |

**Failover Automation Level** (Displayed when DR is in use)

Sets the automation level when a DR failure occurs. Supported levels vary by topology. 

**Standby Node Settings** (Displayed when DR is in use)

Displays the currently configured Standby node list, and allows the following items to be changed.

| Item | Description |
| --- | --- |
| Open Mode | Sets the Open Mode of the Standby node. <br>`Recovery` or `Read Only` can be selected. |
| Log Replication Type | Sets the log replication method for the Standby node. <br>`LGWR ASYNC` or `ARCH ASYNC` can be selected. |
{% endtab %}
{% tab title="Instance Configuration" %}
Some items may not be displayed depending on the topology and installation/registration method.

| Field | Description | Notes |
| --- | --- | --- |
| Hostname | Connected host information | Not editable |
| Service IP | Directly enter or select the IP to be used for communication between OwlDB and the node. | Not editable |
| Service Port | Directly enter the port to be used for communication between OwlDB and the database server. | Not editable |
| Interconnect IP | Select from the list the Interconnect IP to be used for communication between nodes within the cluster. | Not editable |
| Primary Destination IP<br>(Enter for Primary instance only) | Directly enter the Primary Destination IP to be used for communication from StandBy DB to Primary DB. | Not editable |
| Primary Destination Port<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to be used for communication from StandBy DB to Primary DB. | Not editable |
| StandBy Destination IP<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to be used for communication from Primary DB to StandBy DB. | Not editable |
| StandBy Destination Port<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination Port to be used for communication from Primary DB to StandBy DB. | Not editable |
| Data Path | Enter Data Path | Not editable |
| Redo Path | Enter Redo Path | Not editable |
| Archive Path | Enter Archive Path | Not editable |
| Backup Path* | Enter Backup Path | Only file system paths can be entered |
| SSH Port | SSH port | Not editable |
| SSH User | SSH User | Not editable |
| SSH Password | SSH Password | Not editable |

Only the Backup Path can be modified during the instance configuration step.

**Backup Path**only accepts file system paths, and in the case of a TAC configuration, **shared volume**must be used.

Configuration information for each Primary / Standby node is displayed according to the configuration set in the previous step. When scaling out, input fields for the added nodes are newly created; when scaling in, the corresponding nodes are removed from the screen.
{% endtab %}
{% tab title="Database Configuration" %}
This is the step for entering database configuration information.

| Field | Description |
| --- | --- |
| Database Name | Name of the database to use |
| SYS User Password | Password for the highest-privilege database administrator account (SYS user) |
| Target Memory Size | Target memory size |
| Shared Memory Size | Shared memory size |
| Character Set | Character encoding to use for the database |
| Timezone | OS timezone where the database will be installed |
| VIP | Select whether to use VIP |
| Primary Node #N Vip* | Database virtual IP<br>(Activated when VIP use is selected) |
| Database Listener Port | Database listener port for network communication |
| Max Session Count | Maximum number of concurrent sessions allowed |
| Redo Log File Size (MB) | Redo log file size |
| System Data File Size (MB) | Size of the data file for storing system tables and key metadata |
| Syssub Data File Size (MB) | Sub data file size for storing system operation-related data |
| User Tablespace Data File Size (MB) | Tablespace data file size for storing user data |
| Temporary Tablespace Data File Size (MB) | Temporary tablespace data file size used for large-scale operations |
| Undo Tablespace Data File Size (MB) | Undo tablespace size |

This is the step for reviewing database configuration information. Most fields are automatically populated from OwlDB metadata and actual DB discovery data. If a scale-out occurs on a DB that uses VIP, the VIP for the added node must be entered at this step.
{% endtab %}
{% tab title="Configuration Review" %}
Review the final settings configured in the previous step. Changed fields are highlighted in blue, and each field can be expanded or collapsed using the accordion. **Complete** Click the button to apply the spec changes.

{% hint style="warning" %}
**Caution**

If there are no changes, the Complete button will be disabled.

If you change the DR configuration to disabled while retired instances exist in Standby, a confirmation modal will appear. Upon confirmation, all retired instances will be deleted and the DR configuration will be changed to disabled.
{% endhint %}
{% endtab %}
{% endtabs %}

---

## **Entering spec change from a change-detected DB**

For registered DBs only, if the DB configuration is changed outside of OwlDB, OwlDB automatically detects this. You can check the change-detected DB in the dashboard explorer, and **Spec Change** click the button to enter the spec change page.

When entering via this method, the externally changed details are automatically reflected on the spec change page. Changed fields are marked separately, and users can review the content before applying it to OwlDB.

**Example**) When a TAC DR DB using VIP (Primary 2 nodes / Standby 1 node) has its Primary nodes externally expanded to 4:

1. **Engine Options** : The 2 added nodes are displayed in the list.
2. **Instance Configuration** : Fields for entering configuration information of the 2 added nodes are created.
3. **Database Configuration** : Fields for entering the VIP of the 2 added nodes are created.

After reviewing and completing the input at each step, **Complete** click the button to apply the changes to OwlDB.



## Maximum Processing Time for Spec Changes

The processing time for spec changes may vary depending on the database size, load status, and configuration environment. In a typical environment, processing completes within a few minutes; however, the maximum processing time may differ based on conditions as shown below.

{% tabs %}
{% tab title="Primary Creation" %}
| Logic | Maximum Processing Time | Remarks |
| --- | --- | --- |
| Database Configuration | 6 hours | Script Execution |
{% endtab %}
{% tab title="Primary Removal" %}
| Logic | Maximum Processing Time | Remarks |
| --- | --- | --- |
| Database stop and cluster resource removal | 30 minutes |   |
| Environment cleanup | 5 minutes |   |
{% endtab %}
{% tab title="Standby Creation" %}
| Logic | Maximum Processing Time | Remarks |
| --- | --- | --- |
| CM creation on Single Database | 30 minutes | Database stop |
|   | 6 hours | Cluster resource addition |
|   | 30 minutes | Database startup |
| Primary node backup | 6 hours |   |
| Standby node configuration | 6 hours |   |
| Primary node parameter change | 30 minutes | Database stop |
|   |   | Add parameter to tip |
|   | 30 minutes | Database startup |
{% endtab %}
{% tab title="Standby Removal" %}
| Logic | Maximum Processing Time | Remarks |
| --- | --- | --- |
| Database stop and cluster resource removal | 30 minutes |   |
| Environment cleanup | 5 minutes |   |
{% endtab %}
{% endtabs %}
