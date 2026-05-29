# Instance

**OwlDB**You can monitor the status of instances running in OwlDB, and modify or restart instances as needed. Buttons allow you to quickly perform desired actions. If the instance status is `Available`not the case, some information may be missing. 

{% hint style="info" %}
**Note**

You can navigate to the instance management page from the dashboard via the following path.

1. List view: **Arrow icon next to the database alias > Instance alias** click
2. Card view: On the database card, **Instance alias** click
{% endhint %}

## **Viewing Instance Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose instance information you want to view.
3. **Instance **Click the tab.
4. In the instance list, click the 'instance alias' whose information you want to view.
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
| Maximum connection sessions | Current usage of maximum connection sessions |
| Instance Id | Identifier that distinguishes the current DB node (instance) |
| End Point | Connection address for clients to connect to the database |
{% endtab %}
{% tab title="Standby" %}
| Item | Description |
| --- | --- |
| Instance status | Health value |
| Role | Standby Mode value<br>- **Standby,Recovery**<br>- **Standby,Read Only** |
| Instance creation date | yyyy.mm.dd HH:mm:ss |
| Operation mode | OPEN MODE value<br>**- MOUNTED<br>- RECOVERY<br>- READ WRITE<br>- READ ONLY<br>- READ ONLY WITH APPLY** |
| Last updated date | yyyy.mm.dd HH:mm:ss |
| Port | The port number on which the database service receives communications (listener port) |
| Log Replication Mode | Method of transmitting the Primary's log to the Standby<br>**- LGWR ASYNC<br>- ARCH ASYNC** |
| Standby Status | - PRIMARY NOT CONNECTED<br>- RRIMARY CONNECTED, RECOVERY NOT STARTED<br>- PRIMARY CONNECTED, STARTING RECOVERY<br>- READ-ONLY STANDBY, RECOVERY IN PROGRESS<br>- STANDBY, RECOVERY IN PROGERSS<br>- READ-ONLY STANDBY, RECOVERY SUSPENDED<br>- STANDBY, RECOVERY SUSPENDED<br>- PRIMARY DISCONNECTED, FINISHING RECOVERY |
| Log Last Received | TSN of the most recently received Redo Log from the Primary |
| Log Last Applied | TSN of the most recently applied (recovered) Redo Log on the Standby |
| Replication Lag (TSN Diff) | TSN difference from the Primary Database (integer) |
| CPU | Current CPU usage |
| Memory | Current Memory usage |
| Maximum number of concurrent sessions | Current usage of maximum concurrent sessions |
| Instance Id | An identifier that distinguishes the current DB node (instance) |
| End Point | The connection address used by clients to connect to the database |
{% endtab %}
{% endtabs %}



---

## **Edit Instance Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose instance information you want to view.
3. **Instance **Click the tab.
4. In the instance list, click the 'Instance Alias' whose information you want to view.
5. Next to the 'Instance Alias' **pencil icon**Click it.
6. Edit the instance alias and description.
7. **Save** Click the button.



---

## **Restart Instance**

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

**Conditions under which restart is available**

When the instance status is `Available`[T_41]
When the database status is

데이터베이스 상태가 `Degraded`and the instance status is `Limited`[T_44]
When the database status is

데이터베이스 상태가 `Degraded` or `Down`and the instance status is `Unavailable`[T_48]
However, cases where the database status code includes

- 단, 데이터베이스 상태 코드에 `VM Down` or `Agent Disconnect`are excluded

When the topology type is `Single+DR`, the instance role is `Standby`, and the instance status is `Retired`
{% endhint %}



---
