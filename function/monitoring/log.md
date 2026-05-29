# Syslog

You can view information on various events and processes occurring in the system.

1. **OwlDB Console > Monitoring > Log Monitoring > Syslog** Navigate to the menu.
2. **DB Alias**, **Instance Alias** Click the dropdown button to select the database and instance to monitor.
3. View the log list. You can filter by setting a query period. You can search for messages directly to view them.



---

# Bootlog

You can diagnose the cause of issues by viewing status and error information related to the boot process.

1. **OwlDB Console > Monitoring > Log Monitoring > Bootlog** Navigate to the menu.
2. **DB Alias**, **Instance Alias** Click the dropdown button to select the database and instance to monitor.
3. View the log list. You can filter by setting a query period. You can filter by event, mode, and status.
4. Click a message to view its details.



---

# Eventlog

You can view information such as warnings and errors occurring in the database.

{% hint style="info" %}
**Note**

You can monitor multiple databases and instances simultaneously by selecting them at the same time.
{% endhint %}

1. **OwlDB Console > Monitoring > Log Monitoring > Eventlog** Navigate to the menu.
2. **DB Alias**, **Instance Alias** Click the dropdown button to select the database and instance to monitor.
3. View the log list. You can filter by setting a query period. You can filter by status. You can filter by message.

| Status | Condition |
| --- | --- |
| Info | When the instance status changes |
| Warning | When CPU usage exceeds 50% |
|   | When Memory usage exceeds 50% |
| Error | When CPU usage exceeds 90% |
|   | When Memory usage exceeds 90% |

{% hint style="info" %}
**Note**

**OwlDB Console > Dashboard > Eventlog** > **View Details**Click to navigate to the Eventlog page.
{% endhint %}
