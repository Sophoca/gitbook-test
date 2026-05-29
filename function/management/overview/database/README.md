# Feature Usage Guide / Management / Overview / Database

You can monitor the status of databases running in OwlDB, and modify, stop, start, delete, switch roles, and change specs of databases as needed. You can quickly perform desired operations via buttons, and adjust various settings to optimize database performance. If the instance status is `Running`other than , some information may be missing. 

{% hint style="info" %}
**Note**

The database management page displays time based on the database timezone, so there may be a difference from the local system time (browser time).
{% endhint %}

---

## **Viewing Database Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias **Click the dropdown button to select the database whose information you want to view.
3. Check detailed information in the Database, Instance, Version, and (DR) Switchover History Management tabs.
4. For the database operational status, [**Overall Status Summary**](#undefined)** **page,** **please refer to.

{% tabs %}
{% tab title="데이터베이스" %}
You can view detailed database information such as account information accessible to the database, control files, logs, and checkpoints, and visually confirm the database configuration as a diagram.
{% endtab %}
{% tab title="인스턴스" %}
View the list and information of configured instances.

- Clicking 'Instance Alias' navigates to the [**Instance Management**](function/management/overview/instance.md) page.
- Click the ☑️ icon to restart one or more instances simultaneously.  [**For Instance Restart,**](#undefined-2)please refer to.

{% hint style="info" %}
**Note**

When using a DR configuration, Primary DB and Standby DB are queried separately.
{% endhint %}
{% endtab %}
{% tab title="버전" %}
View database version information, system and compilation information, and patch information.
{% endtab %}
{% tab title="(DR) 전환 이력 관리" %}
This is a tab provided in DR configurations.

View the history of database role switchover events.

- Data added after a switchover event has occurred and completed

| Column Name | Description | Data Format | Default Value | Required |
| --- | --- | --- | --- | --- |
| Start Time | The time when the switchover event occurred | yyyy.mm.dd HH:mm:ss | O | O |
| End Time | The time when the switchover event completed | yyyy.mm.dd HH:mm:ss | X | X |
| Type | Switchover event type | • Failover<br>• Switchover<br>• Failback | O | O |
| Target | The target that performed the event | • Role Switchover: {user ID}<br>• Automated Failover: System / {user ID} | O | X |
| Result | Displays the status of the event | • Success<br>• Failure | O | X |
| Cause/Remarks | Displays the cause of the event or the value entered by the user | • Role Switchover<br>• Optionally entered by the user when requesting a role switchover (maximum 200 characters)<br>• If not entered: displayed as blank<br>• Automated Failover<br>• Specifies the trigger condition<br>• Optionally entered by the user when requesting manually | O | X |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**

**OwlDB console screen > Dashboard > DB Alias**Click to navigate to the database management page.
{% endhint %}



---

## **Modifying Database Information**

1. **OwlDB console screen > Management** **> Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose information you want to edit.
3. Next to 'Database Alias' **pencil icon**click it.
4. Edit the database alias and description.
5. **Save **Click the button.



---
