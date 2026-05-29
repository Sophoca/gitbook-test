# Feature Usage Guide / Management / Overview / Instance

**OwlDB**You can monitor the status of instances running in OwlDB, and modify or restart instances as needed. Buttons allow you to quickly perform desired operations. If the instance status is not `Available`, some information may be missing. 

{% hint style="info" %}
**Note**

You can navigate to the instance management page from the dashboard via the following paths.

1. List view: **Arrow icon next to the database alias > Instance alias** click
2. Card view: On the database card, **Instance alias** click
{% endhint %}

## **Viewing Instance Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose instance information you want to view.
3. **Instance **Click the tab.
4. In the instance list, click the 'Instance alias' whose information you want to view.
5. Review the instance detail information.

{% tabs %}
{% tab title="Primary " %}
| Item | Description |
| --- | --- |
| Instance status | Health value |
| Role | Primary |
| Instance creation date | yyyy.mm.dd HH:mm:ss |
| Operation mode | OPEN MODE value<br>- **READ WRITE** |
| Last updated date | yyyy.mm.dd HH:mm:ss |
| Port | Port number on which the database service receives communications (listener port) |
| Replication Mode | PERFORMANCE |
| Current Log | TSN of the most recent Redo Log |
| CPU | Current CPU usage |
| Memory | Current Memory usage |
| Maximum number of connected sessions | Current usage of the maximum number of connected sessions |
| Instance Id | Identifier that distinguishes the current DB node (instance) |
| End Point | Connection address for clients to connect to the database |
{% endtab %}
{% tab title="Standby" %}
| Item | Description |
| --- | --- |
| Instance status | Health value |
| Role | Standby Mode value<br>- **Standby, Recovery**<br>- **Standby, Read Only** |
| Instance creation date | yyyy.mm.dd HH:mm:ss |
| Operation mode | OPEN MODE value<br>**- MOUNTED<br>- RECOVERY<br>- READ WRITE<br>- READ ONLY<br>- READ ONLY WITH APPLY** |
| Last updated date | yyyy.mm.dd HH:mm:ss |
| Port | The port number on which the database service listens for communication (listener port) |
| Log Replication Mode | Method by which logs from Primary are transmitted to Standby<br>**- LGWR ASYNC<br>- ARCH ASYNC** |
| Standby Status | - PRIMARY NOT CONNECTED<br>- RRIMARY CONNECTED, RECOVERY NOT STARTED<br>- PRIMARY CONNECTED, STARTING RECOVERY<br>- READ-ONLY STANDBY, RECOVERY IN PROGRESS<br>- STANDBY, RECOVERY IN PROGERSS<br>- READ-ONLY STANDBY, RECOVERY SUSPENDED<br>- STANDBY, RECOVERY SUSPENDED<br>- PRIMARY DISCONNECTED, FINISHING RECOVERY |
| Log Last Received | TSN of the most recently received Redo Log from Primary |
| Log Last Applied | TSN of the most recently applied (recovered) Redo Log on Standby |
| Replication Lag (TSN Diff) | TSN difference from Primary Database (integer) |
| CPU | Current CPU usage |
| Memory | Current Memory usage |
| Maximum number of connected sessions | Current usage of the maximum number of connected sessions |
| Instance Id | An identifier that distinguishes the current DB node (instance) |
| End Point | The connection address used by clients to connect to the database |
{% endtab %}
{% endtabs %}



---

## **Editing Instance Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose instance information you want to view.
3. **Instance **Click the tab.
4. In the instance list, click the 'Instance Alias' whose information you want to view.
5. Next to the 'Instance Alias', **pencil icon**click it.
6. Edit the instance alias and description.
7. **Save** Click the button.



---

## **Restarting an Instance**

{% hint style="warning" %}
**Caution**

When restarting an instance, all currently connected sessions will be terminated. It may take several minutes before the instance becomes active again.
{% endhint %}

1. **OwlDB console screen > Management** **> Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose instance information you want to view.
3. **Instance **Click the tab.
4. In the instance list, click the 'Instance Alias' of the instance you want to restart.
5. **Restart** Click the button.

{% hint style="info" %}
**Note**

**Cases where restart is available**

When the instance status is `Available`in this state

When the database status is `Degraded`and the instance status is `Limited`in this state

When the database status is `Degraded` or `Down`and the instance status is `Unavailable`in this state

- However, cases where the database status code includes `VM Down` or `Agent Disconnect`are excluded

When the topology type is `Single+DR`and the instance role is `Standby`and the instance status is `Retired`in this state
{% endhint %}



---
