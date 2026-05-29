# Feature Usage Guide / Dashboard / Database Restart

For databases in a multi-cluster configuration, you can restart on a per-node basis. The restart progress can be checked by clicking the [:1f514:] icon in the upper right corner of the console screen. This is only available when the instance status is `Available` or the database status is `Degraded` , `Down` .

{% hint style="warning" %}
**Caution**

When restarting the database, all currently connected sessions will be terminated. It may take several minutes before the database becomes active again.
{% endhint %}

1. **Navigate to the OwlDB console screen > Dashboard** menu.
2. Select the database to restart using the radio button, then click the **Restart** button.   For databases in a multi-cluster configuration, select the node to restart.
3. Select the database** **shutdown mode.

{% tabs %}
{% tab title="Tibero" %}
| Category | Description |
| --- | --- |
| NORMAL | (planned for future support) Waits until all session connections are disconnected before shutting down |
| POST_TX | (planned for future support) Waits until all transactions have completed before shutting down |
| IMMEDIATE | Forcibly terminates all currently running operations and rolls back all in-progress transactions before shutting down |
| ABORT | Forcibly terminates Tibero processes |
| ABNORMAL | Forcibly terminates server processes without connecting to the Tibero server (recommended for use in emergency situations only) |

{% hint style="warning" %}
**Caution **

When shutting down in ABORT mode, some system resources (shared memory, semaphores, etc.) may not be released, which may require damage recovery. It is recommended to use this mode only in the following situations:

- When normal shutdown is not possible due to an internal Tibero error
- When Tibero must be shut down immediately due to a hardware problem
- When Tibero must be shut down immediately due to an emergency such as a security breach
{% endhint %}

{% hint style="warning" %}
**Caution**

ABNORMAL mode immediately shuts down the server using an OS forced termination signal, and since system resources (shared memory, semaphores, etc.) are not released, a damage recovery process is required after restart. It is recommended to use this mode only in the following situations:

- When normal shutdown is not possible due to an internal Tibero error
- When a shutdown command has been issued in a mode other than ABNORMAL but is delayed, and an immediate forced shutdown is required
- When shutdown in a mode other than ABNORMAL fails due to external factors such as hardware or OS issues
- When Tibero must be shut down immediately due to an emergency such as a security breach
{% endhint %}
{% endtab %}
{% tab title="Tmax OpenSQL" %}
This feature is planned for future support.
{% endtab %}
{% endtabs %}

1. **Click the Restart** button.
