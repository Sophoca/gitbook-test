# Database

You can monitor the status of databases running in OwlDB, and perform modifications, stop, start, delete, role switching, and spec changes on databases as needed. You can quickly perform desired operations using buttons, and adjust various settings to optimize database performance. If the instance status is `Running`other than , some information may be missing. 

{% hint style="info" %}
**Note**

The database management page displays time based on the database timezone, so there may be a difference from the local system time (browser time).
{% endhint %}

---

## **Viewing Database Information**

1. **OwlDB console screen > Management > Overview** Navigate to the menu.
2. **DB Alias **Click the dropdown button to select the database whose information you want to view.
3. Check detailed information in the Database, Instance, Version, and (DR) Switchover History Management tabs.
4. For the database operational status, [**Overall Status Summary**](#undefined)** **page** **please refer to.

{% tabs %}
{% tab title="Database" %}
You can view detailed database information such as account information accessible to the database, control files, logs, and checkpoints, and visually check the database configuration in a diagram.
{% endtab %}
{% tab title="Instance" %}
View the list of configured instances and their information.

- Clicking 'Instance Alias' navigates to the [**Instance Management**](../instance.md) page.
- Click the ☑️ icon to restart one or more instances simultaneously.  [**Please refer to Instance Restart**](#undefined-2)for more information.

{% hint style="info" %}
**Note**

When using a DR configuration, Primary DB and Standby DB are queried separately.
{% endhint %}
{% endtab %}
{% tab title="Version" %}
View database version information along with system and compilation information, and patch information.
{% endtab %}
{% tab title="(DR) Switchover History Management" %}
This is a tab provided in DR configurations.

View the history of database role switchover events that have occurred.

- Data added after the switchover event has occurred and completed

| Column Name | Description | Data Format | Default Value | Required |
| --- | --- | --- | --- | --- |
| Start Time | The time the switchover event occurred | yyyy.mm.dd HH:mm:ss | O | O |
| Completion Time | The time the switchover event completed | yyyy.mm.dd HH:mm:ss | X | X |
| Type | Switchover event type | • Failover<br>• Switchover<br>• Failback | O | O |
| Target | The target that performed the event | • Role Switchover: {user ID}<br>• Automated Failover: System / {user ID} | O | X |
| Result | Displays the status of the event | • Success<br>• Failure | O | X |
| Cause/Remarks | Displays the cause of the event or the value entered by the user | • Role Switchover<br>• Optionally entered by the user when requesting a role switchover (maximum 200 characters)<br>• If not entered: displayed as blank<br>• Automated Failover<br>• Specifies the trigger condition<br>• Optionally entered by the user when requesting manually | O | X |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**

**OwlDB console screen > Dashboard > DB Alias**You can navigate to the database management page by clicking.
{% endhint %}



---

## **Modifying Database Information**

1. **OwlDB console screen > Administration** **> Overview** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose information you want to modify.
3. Next to 'Database Alias' **pencil icon**click it.
4. Modify the database alias and description.
5. **Save **Click the button.



---
