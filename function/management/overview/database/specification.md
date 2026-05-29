# Feature Usage Guide / Management / Overview / Database / Spec Change

This feature allows you to change the configuration of a running database. Spec changes are possible when the database operational status is `Running` or `Degraded`.

## How to Change Specs

The spec change page can be accessed in the following two ways.

1. **Entering Spec Change from Overview** Overview page > Actions > Click the Spec Change button
2. **Entering Spec Change from Change Detection DB** Dashboard > Explore > Change Detection DB > Click the Spec Change button



## **Entering Spec Change from Overview**

When entering the spec change page through the Actions menu on the Overview page, you can perform the following two operations.

### 1. DB Node Configuration Change

**Installed DB**supports Scale In/Out of Primary nodes within the topology scope of the standard architecture. For example, in a TAC configuration, the number of Primary nodes can be adjusted from a minimum of 2 to a maximum of 4.

If Scale Out has been performed, and the DB is using a VIP, you must enter the VIP for the added node in the **Database Configuration** step of the spec change page.

**Registered DB**does not support Scale In/Out.

{% hint style="info" %}
**Note**

Changing the topology itself (e.g., Single → TAC) is not supported in spec change.

If Scale Out has been performed on a DB using a VIP, you must enter the VIP for the added node in step 4, Database Configuration.
{% endhint %}

### 2. DR Modification

**Installed DB**can be changed between DR enabled ↔ disabled, and the failover automation level can also be changed. If DR is in use, the Open Mode and Log Replication Type of the Standby node can also be changed. 

**Registered DB**does not support changing DR usage, and if DR is in use, only the failover automation level and Standby node settings can be changed.

{% hint style="info" %}
**Note**

For supported failover automation levels, please refer to the [**Failover Automation documentation**](references/failover-automation.md).
{% endhint %}



## **Spec Change Steps**

{% tabs %}
{% tab title="엔진 옵션" %}
This is the step for configuring the database alias, engine, and topology information.

| Item | Description | Remarks |
| --- | --- | --- |
| Database Alias | An alias used to identify the database | Not editable |
| Database Engine Type | The database engine to use<br>- **Tibero**<br>- **Tmax OpenSQL** (planned for future support) | Not editable |
| Topology | The topology type that determines the database structure<br>- **Single**<br>- **TAC** | Not editable |
| Node Count | Number of nodes in the cluster configuration | Not editable |
| Scale In/Out | Primary node list | Available only for Installed DB <br>This list is available |

For TAC topology DBs that are installed, a **Scale In/Out** item is additionally displayed below Node Count.
You can view the currently configured Primary node list and add or remove nodes.

- **Add** : Clicking the Add button allows you to select an instance from the list of installable hosts.
The selected host is added to the Scale In/Out table and becomes a Scale Out target.
- **Delete** : Select the node to remove from the table, then click the Delete button. The selected node becomes a Scale In target and is displayed grayed out in the table.
- **Reset** : Reverts any added or deleted changes back to the initial state.
{% endtab %}
{% tab title="DR 구성" %}
This is the step for configuring DR usage and the failover automation level.

| Item | Description | Remarks |
| --- | --- | --- |
| Enable DR | Whether to use DR configuration | Can only be changed for installed DBs |
| Failover Automation Level | [Automatic failover step](#undefined)<br>- Level 0: Manual<br>- Level 1: Automatic Failover<br>- Level 2: Automatic Configuration Recovery (not supported in OwlDB v1.3) <br>- Level 3: Full Automation | Modifiable |
| Standby Count | Number of Standby DBs | The maximum number of Standby DBs supported in the current standard architecture is 1. |
| Standby Scale In/Out | StandBy Node List | Available when DR is in use |
| Standby Mode | Select the Open Mode option for a StandBy node in the StandBy node list **Recovery**<br>- **Read Only** | - |
| Log Replication Type | Select the log transfer method for a StandBy node in the StandBy node list<br>• **LGWR ASYNC : **A replication mode that transmits Redo logs generated in real time when a transaction occurs<br>• **ARCH ASYNC : **A replication mode that collects and transmits archive log files after a log switch occurs | - |

This is the step where you can change DR usage, failover automation level, and Standby node settings.

**DR Usage** (Can only be changed for installed DBs)

| Change Direction | Action |
| --- | --- |
| Disabled → Enabled | Proceeds with new Standby node provisioning; sets failover automation level to default level 1 |
| Enabled → Disabled | Proceeds with Standby node clean up |

**Failover Automation Level** (Displayed when DR is in use)

Sets the automation level when a DR failure occurs. Supported levels vary by topology. 

**Standby Node Settings** (Displayed when DR is in use)

Displays the currently configured Standby node list, and allows modification of the following items.

| Item | Description |
| --- | --- |
| Open Mode | Sets the Open Mode of the Standby node. <br>`Recovery` or `Read Only` can be selected. |
| Log Replication Type | Sets the log replication method of the Standby node. <br>`LGWR ASYNC` or `ARCH ASYNC` can be selected. |
{% endtab %}
{% tab title="인스턴스 구성" %}
Some items may not be displayed depending on the topology and installation/registration method.

| Field | Description | Notes |
| --- | --- | --- |
| Hostname | Connected host information | Not editable |
| Service IP | Directly enter or select the IP to be used for communication between OwlDB and the node. | Not editable |
| Service Port | Directly enter the Port to be used for communication between OwlDB and the database server. | Not editable |
| Interconnect IP | Select the Interconnect IP to be used for communication between nodes within the cluster from the list. | Not editable |
| Primary Destination IP<br>(Enter for Primary instance only) | Directly enter the Primary Destination IP to be used for communication from StandBy DB to Primary DB. | Not editable |
| Primary Destination Port<br>(Enter for Primary instance only) | Directly enter the Primary Destination Port to be used for communication from StandBy DB to Primary DB. | Not editable |
| StandBy Destination IP<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination IP to be used for communication from Primary DB to StandBy DB. | Not editable |
| StandBy Destination Port<br>(Enter for StandBy instance only) | Directly enter the StandBy Destination Port to be used for communication from Primary DB to StandBy DB. | Not editable |
| Data Path | Enter the data path. | Not editable |
| Redo Path | Enter the Redo path. | Not editable |
| Archive Path | Enter Archive Path | Not editable |
| Backup Path* | Enter Backup Path | Only file system paths can be entered |
| SSH Port | SSH port | Not editable |
| SSH User | SSH User | Not editable |
| SSH Password | SSH Password | Not editable |

Only the Backup Path can be modified during the instance configuration step.

**Backup Path**only accepts file system paths, and in a TAC configuration it must be configured as a **shared volume**.

Configuration information for each Primary / Standby node is displayed according to the configuration set in the previous step. When scaling out, input fields for the newly added nodes are created; when scaling in, the corresponding nodes are removed from the screen.
{% endtab %}
{% tab title="데이터베이스 구성" %}
This step is for entering database configuration information.

| Field | Description |
| --- | --- |
| Database Name | Name of the database to use |
| SYS User Password | Password for the highest-privilege database administrator account (SYS user) |
| Target Memory Size | Target memory size |
| Shared Memory Size | Shared memory size |
| Character Set | Character encoding to use for the database |
| Timezone | OS timezone of the environment where the database will be installed |
| VIP | Select whether to use VIP |
| Primary Node #N Vip* | Database virtual IP<br>(Enabled when VIP usage is selected) |
| Database Listener Port | Database listener port for network communication |
| Max Session Count | Maximum number of concurrent sessions allowed |
| Redo Log File Size (MB) | Redo log file size |
| System Data File Size (MB) | Size of the data file for storing system tables and key metadata |
| Syssub Data File Size (MB) | Sub data file size for storing system operation-related data |
| User Tablespace Data File Size (MB) | Size of the tablespace data file for storing user data |
| Temporary Tablespace Data File Size (MB) | Size of the temporary tablespace data file used for large-scale operations |
| Undo Tablespace Data File Size (MB) | Undo tablespace size |

This step is for reviewing database configuration information. Most fields are populated automatically from OwlDB metadata and actual DB discovery data. If a Scale Out occurs on a DB that uses VIP, the VIP for the added nodes must be entered at this step.
{% endtab %}
{% tab title="구성 정보 확인" %}
Review the configuration set in the previous step for final confirmation. Changed fields are highlighted in blue, and each field can be expanded or collapsed using the accordion. **Complete** Click the button to apply the spec changes.

{% hint style="warning" %}
**Caution**

If there are no changes, the Complete button will be disabled.

If you change the DR configuration to disabled while there are Retired instances on the Standby, a confirmation modal will appear. Upon confirmation, all Retired instances will be permanently deleted and the DR configuration will be set to disabled.
{% endhint %}
{% endtab %}
{% endtabs %}

---

## **Entering spec change from a change-detected DB**

For registered DBs only, if the DB configuration is changed outside of OwlDB, OwlDB automatically detects this. You can check the change-detected DB in the dashboard discovery view, and **Spec Change** click the button to navigate to the spec change page.

When entering via this method, the externally changed details are automatically reflected on the spec change page. Changed fields are indicated separately, and users can review the content before applying it to OwlDB.

**Example**) For a TAC DR DB using VIP (Primary 2 nodes / Standby 1 node), if the Primary nodes are increased to 4 externally:

1. **Engine Options** : The 2 added nodes are displayed in the list.
2. **Instance Configuration** : Input fields for entering the configuration information of the 2 added nodes are created.
3. **Database Configuration** : A field is created for entering the VIP of the 2 added nodes.

After reviewing the content at each step and completing the input, **Complete** click the button to apply the changes to OwlDB.



## Maximum Processing Time for Spec Changes

The processing time for spec changes may vary depending on the database capacity, load status, and configuration environment. In a typical environment, processing completes within a few minutes; however, the maximum processing time may differ depending on conditions as shown below.

{% tabs %}
{% tab title="Primary 생성" %}
| Logic | Maximum Processing Time | Notes |
| --- | --- | --- |
| Database Configuration | 6 hours | Script Execution |
{% endtab %}
{% tab title="Primary 제거" %}
| Logic | Maximum Processing Time | Notes |
| --- | --- | --- |
| Stop Database and Remove Cluster Resources | 30 minutes |   |
| Environment Cleanup | 5 minutes |   |
{% endtab %}
{% tab title="Standby 생성" %}
| Logic | Maximum Processing Time | Notes |
| --- | --- | --- |
| Create CM on Single Database | 30 minutes | Stop Database |
|   | 6 hours | Add Cluster Resources |
|   | 30 minutes | Start Database |
| Backup Primary Node | 6 hours |   |
| Configure Standby Node | 6 hours |   |
| Change Primary Node Parameters | 30 minutes | Stop Database |
|   |   | Add Parameters to tip |
|   | 30 minutes | Start Database |
{% endtab %}
{% tab title="Standby 제거" %}
| Logic | Maximum Processing Time | Notes |
| --- | --- | --- |
| Stop Database and Remove Cluster Resources | 30 minutes |   |
| Environment Cleanup | 5 minutes |   |
{% endtab %}
{% endtabs %}
