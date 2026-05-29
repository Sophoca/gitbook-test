# Dashboard

Provides summary information and alerts on the status of all databases and instances in operation. 

**OwlDB console screen > Click the OwlDB logo**to view the dashboard.

## **Overall status summary**

View the top-level status value (**Status**) and the detailed status value (**Health**) for all databases/instances in operation. Clicking each status will display the list of databases/instances with that status value in the 'Database List'. 

{% tabs %}
{% tab title="Status" %}
The top-level status, Status, is displayed at the database level.

- Since the status may change per instance node, the count is displayed next to the status in the format (n/m). n: Number of available instance nodes m: Total number of instance nodes
- **Bold *** indicates a type that can be filtered on the dashboard.

| Type | Description |
| --- | --- |
| Deploying | The database is being installed. |
| **Running *** | The database is available for normal use. |
| **Updating *** | A task is being performed on the database or changes are being applied. |
| **Degraded *** | Some databases or components are unavailable. |
| **Failover *** | The system has detected a database failure and Auto Failover is in progress. |
| **Down *** | The database is unavailable. |
| Starting | Transitioning from Stopped to Running. |
| Stopping | Transitioning from Running to Stopped. |
| Stopped | All resources are temporarily inactive. <br>(Resources deactivated) |
| Terminating | All resources and data are being permanently deleted. <br>(Upon completion, access and recovery are not possible.) |
{% endtab %}
{% tab title="Health" %}
The detailed status, Health, is displayed per instance node.

- Displayed as a combination of DB Boot mode, Instance, cluster management tool (hereafter CMT), and Agent connection status.
- Features restricted by each message can be confirmed via a banner upon entering the respective menu.

| Type | Message | Description |
| --- | --- | --- |
| 🟢 Available | - | Node is in a normal state. |
| 🟡 Limited | CMT Inactive | Cluster management tool is in an abnormal state. |
|   | Mount Mode | The node has started in Mount mode. |
| 🔴 Unavailable | Nomount Mode / DB Down | The node has started in Nomount mode or is Down. |
|   | Agent Disconnect | The connection to the VM where the node is located has been lost. |
|   | VM Down | The VM where the node is located is Down. |
| 🔵 In Progress | Reboot | The node is restarting. |
|   | Switchover | The node is undergoing a role switch. |
|   | Failover | The node is undergoing failover. |
|   | Rebuilding | The node is being rebuilt. |
|   | Modify Spec | The node's configuration or specifications are being changed. |
|   | Migration | State in which data is being migrated to a node |
|   | Restoring | State in which a node is being restored |
| ⚫ Retired | Retired | The (former) Primary has terminated abnormally during a Failover process. |

{% hint style="info" %}
**Notice**

A cluster management tool is a component required to operate a database in a cluster configuration.
(e.g., Tibero Cluster Manager (CM), Tibero Active Storage (TAS), etc.)
{% endhint %}
{% endtab %}
{% endtabs %}



---

## **Database**/Instance** View List**

View the full list of databases and their subordinate instances. '[View Overall Status Summary](#undefined)' The list of databases and instances displayed varies depending on the status value selected.

- You can perform restart operations on the subordinate instances of the selected database.
- You can perform start, stop, delete, role switch, and license renewal management operations on the selected database.
- Provides a search function for database/instance aliases.
- Administrators can query databases that are registrable, have configuration changes, or have specification changes.
- Administrators can query installable hosts.

### Toggle List View (Card View / List View)

The database/instance list can be viewed in two ways: card view and list view.

{% tabs %}
{% tab title="Card View" %}
Card view displays key database information in individual card format for easy visual reference.

| Item | Description |
| --- | --- |
| Database Alias | Displays the number of instances associated with the database alias<br>• When clicked, navigates to the '[Database Management](#3LK7eQbc2EsNjF1sUyV3)' page |
| Database Information | Summarizes and displays key database information at the top of the card<br>• Display Items<br>• Type: Database engine type (Tibero / OpenSQL)<br>• Configuration: Database topology (Single / TAC) → Displays '(+ DR)' when DR is configured<br>• Eventlog: I / W / E (representing Info / Warning / Error respectively)<br>→ When clicked, navigates to the '[Log Monitoring > Eventlog](#eventlog)' page<br>• Statistics reference time: Previous day (00:00–23:59) |
| Instance Information | Displays instance information associated with the database<br>• Display Items<br>• Role: Primary / Standby (Read Only) / Standby (Recovery)<br>• Status: Instance health status<br>• CPU: Current CPU usage (%)<br>• Memory: Current memory usage (%)<br>• Active Sessions: Current number of active sessions (not displayed for Standby (Recovery))<br>• Data Volume: Data Volume usage |
{% endtab %}
{% tab title="List View" %}
List view displays database and subordinate instance information in a tree-structured table for easy hierarchical reference.

{% hint style="info" %}
**Note**
'Default display' refers to items shown by default on the initial screen; 'Required display' refers to items that cannot be hidden.
{% endhint %}

| Item | Database Level | Instance Level | Default Display | Required Display |
| --- | --- | --- | --- | --- |
| **Alias** | Database alias<br>• When clicked, [Database Management](#3LK7eQbc2EsNjF1sUyV3) navigates to the page | Instance alias<br>• When clicked, [Instance Management](#dF57s45IXBUgU7RX1UvL) navigates to the page | O | O |
| **Creation Date** | Database creation date | Instance creation date | X | X |
| **Status** | Database status (Status value) | Instance status (Health value) | O | O |
| **Type** | Database engine type (Tibero / OpenSQL) | No information ('–' displayed) | O | X |
| **Configuration** | Database Topology<br>• Single<br>• TAC<br>• When DR is configured, '(+ DR)' is displayed | Instance Role<br>• Primary<br>• Standby(Read Only)<br>• Standby(Recovery) | O | O |
| **Availability Zone** | No information ('–' displayed) | Availability zone information where the instance is located | O | X |
| **CPU** | No information ('–' displayed) | Current CPU usage (%) | O | X |
| **Memory** | No information ('–' displayed) | Current Memory usage (%) | O | X |
| **Active Sessions** | No information ('–' displayed) | Number of active sessions (not displayed for Standby(Recovery)) | O | X |
| **Volume** | No information ('–' displayed) | Total and usage of Root + Data + Redo log + Archive log Volume | X | X |
| **Data Volume** | No information ('–' displayed) | Data Volume usage | O | X |
| **Redo log Volume** | No information ('–' displayed) | Redo log Volume usage | X | X |
| **Archive log Volume** | No information ('–' displayed) | Archive log Volume usage | X | X |
| **Root Volume** | No information ('–' displayed) | Root Volume usage | X | X |
{% endtab %}
{% endtabs %}

---

## **Viewing Real-Time Charts**

View real-time charts for the top 5 instances per item. 

| Item | Description |
| --- | --- |
| CPU Usage (%) | Real-time CPU usage |
| Memory Usage (%) | Real-time Memory usage |
| Session Load (%) | `(Active Session Count/Max Session Count)X100`A metric indicating the session load level |



---

## **Auto Refresh**

For real-time updates on the dashboard screen, it is automatically refreshed every 5 seconds.
