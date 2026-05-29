# Feature Usage Guide / Dashboard

Provides summary information and notifications about the status of all databases and instances in operation. 

**OwlDB console screen > OwlDB logo**Click to view the dashboard.

## **Overall status summary**

Check the top-level status value (**Status**) and the detailed status value (**Health**) for all databases/instances in operation. Clicking each status allows you to view the list of databases/instances with that status value in the 'Database List'. 

{% tabs %}
{% tab title="Status" %}
The top-level status, Status, is displayed at the database level.

- Because the status may change per instance node, the count is displayed next to the status in the format (n/m). n: number of available instance nodes m: total number of instance nodes
- **Bold *** indicates a type that can be filtered on the dashboard.

| Type | Description |
| --- | --- |
| Deploying | The database is being installed. |
| **Running *** | The database is available for normal use. |
| **Updating *** | An operation is being performed on the database or changes are being applied. |
| **Degraded *** | Some databases or components are unavailable. |
| **Failover *** | The system has detected a database failure and Auto Failover is in progress. |
| **Down *** | The database is unavailable. |
| Starting | Transitioning from Stopped to Running. |
| Stopping | Transitioning from Running to Stopped. |
| Stopped | All resources are temporarily inactive. <br>(Resources deactivated) |
| Terminating | All resources and data are being permanently deleted. <br>(Once complete, access and recovery are not possible.) |
{% endtab %}
{% tab title="Health" %}
The detailed status, Health, is displayed per instance node.

- Displayed as a combination of DB Boot mode, Instance, cluster management tool (hereafter CMT), and Agent connection status.
- Features restricted by each message can be confirmed via a banner upon entering the respective menu.

| Type | Message | Description |
| --- | --- | --- |
| 🟢 Available | - | Node is in a normal state. |
| 🟡 Limited | CMT Inactive | Cluster management tool is in an abnormal state. |
|   | Mount Mode | Node has started in Mount mode. |
| 🔴 Unavailable | Nomount Mode / DB Down | Node has started in Nomount mode or is Down. |
|   | Agent Disconnect | Connection to the VM where the node resides has been lost. |
|   | VM Down | The VM where the node resides is Down. |
| 🔵 In Progress | Reboot | Node is restarting. |
|   | Switchover | Node is undergoing a role switch. |
|   | Failover | Node is undergoing failover. |
|   | Rebuilding | Node is being rebuilt. |
|   | Modify Spec | The node's configuration or spec is being changed. |
|   | Migration | Data is being migrated to the node. |
|   | Restoring | State in which a node is being restored |
| ⚫ Retired | Retired | During the Failover process, the (former) Primary has terminated abnormally. |

{% hint style="info" %}
**Note**

Cluster management tools are components required to operate databases in a cluster configuration.
(e.g., Tibero Cluster Manager (CM), Tibero Active Storage (TAS), etc.)
{% endhint %}
{% endtab %}
{% endtabs %}



---

## **Database**/Instance** List View**

View the full list of databases and their subordinate instances. '[View overall status summary](#undefined)' The list of databases and instances displayed varies depending on the status value selected.

- You can perform a restart operation on the subordinate instances of the selected database.
- You can perform start, stop, delete, role switch, and license renewal management operations on the selected database.
- Provides a search function for database/instance aliases.
- Administrators can query databases that are registerable, configuration-changeable, or spec-changeable.
- Administrators can query installable hosts.

### Toggle list view (Card View / List View)

The database/instance list can be viewed in two formats: card view and list view.

{% tabs %}
{% tab title="카드뷰(Card View)" %}
Card view presents each database as an individual card, making it easy to visually grasp key database information.

| Item | Description |
| --- | --- |
| Database alias | Displays the number of instances associated with the database alias<br>• On click, '[Database Management](#3LK7eQbc2EsNjF1sUyV3)' page opens |
| Database information | Summarizes key database information at the top of the card<br>• Display items<br>• Type: Database engine type (Tibero / OpenSQL)<br>• Configuration: Database topology (Single / TAC) → Displays '(+ DR)' when DR is configured<br>• Eventlog: I / W / E (representing Info / Warning / Error respectively)<br>→ On click, '[Log Monitoring > Eventlog](#eventlog)' page opens<br>• Statistics reference period: Previous day (00:00–23:59) |
| Instance information | Displays information for instances associated under the database<br>• Display items<br>• Role: Primary / Standby (Read Only) / Standby (Recovery)<br>• Status: Instance health status<br>• CPU: Current CPU usage (%)<br>• Memory: Current memory usage (%)<br>• Active Sessions: Current number of active sessions (not displayed for Standby (Recovery))<br>• Data Volume: Data Volume usage |
{% endtab %}
{% tab title="리스트뷰(List View)" %}
List view displays database and subordinate instance information in a tree-structured table for easy hierarchical navigation.

{% hint style="info" %}
**Note**
'Default display' refers to items shown by default on the initial screen; 'Required display' refers to items that cannot be hidden.
{% endhint %}

| Item | Database Level | Instance Level | Default Display | Required Display |
| --- | --- | --- | --- | --- |
| **Alias** | Database alias<br>• On click, [Database Management](#3LK7eQbc2EsNjF1sUyV3) page opens | Instance alias<br>• On click, [Instance Management](#dF57s45IXBUgU7RX1UvL) page opens | O | O |
| **Created date** | Database creation date | Instance creation date | X | X |
| **Status** | Database status (Status value) | Instance status (Health value) | O | O |
| **Type** | Database engine type (Tibero / OpenSQL) | No information ('–' displayed) | O | X |
| **Configuration** | Database topology<br>• Single<br>• TAC<br>• Displays '(+ DR)' when DR is configured | Instance Role<br>• Primary<br>• Standby(Read Only)<br>• Standby(Recovery) | O | O |
| **Availability Zone** | No information ('–' displayed) | Availability zone information where the instance is located | O | X |
| **CPU** | No information ('–' displayed) | Current CPU usage (%) | O | X |
| **Memory** | No information ('–' displayed) | Current memory usage (%) | O | X |
| **Active Sessions** | No information ('–' displayed) | Number of active sessions (not displayed for Standby(Recovery)) | O | X |
| **Volume** | No information ('–' displayed) | Total and usage of Root + Data + Redo log + Archive log Volume | X | X |
| **Data Volume** | No information ('–' displayed) | Data Volume usage | O | X |
| **Redo log Volume** | No information ('–' displayed) | Redo log Volume usage | X | X |
| **Archive log Volume** | No information ('–' displayed) | Archive log Volume usage | X | X |
| **Root Volume** | No information ('–' displayed) | Root Volume usage | X | X |
{% endtab %}
{% endtabs %}

---

## **Real-time Chart View**

View real-time charts for the top 5 instances per item. 

| Item | Description |
| --- | --- |
| CPU Usage (%) | Real-time CPU usage |
| Memory Usage (%) | Real-time memory usage |
| Session Load (%) | `(Active Session Count/Max Session Count)X100`, a metric indicating the session load level |



---

## **Auto Refresh**

The dashboard screen is automatically refreshed every 5 seconds for real-time updates.
