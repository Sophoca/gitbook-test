# Database Restart

For databases with a multi-cluster configuration, you can restart on a per-node basis. You can check the restart progress by clicking the [:1f514:] icon in the upper right corner of the console screen. This is only available when the instance status is `Available` or the database status is `Degraded` , `Down` .

{% hint style="warning" %}
**Caution**

When restarting the database, all currently connected sessions will be terminated. It may take a few minutes before the database becomes active again.
{% endhint %}

1. **Navigate to the OwlDB console screen > Dashboard** menu.
2. Select the database to restart using the radio button, then click the **Restart** button.   For databases with a multi-cluster configuration, select the node to restart.
3. Select the database** **shutdown mode.

{% tabs %}
{% tab title="Tibero" %}
| Category | Description |
| --- | --- |
| NORMAL | (Support planned) Waits until all session connections are disconnected before shutting down |
| POST_TX | (Support planned) Waits until all transactions have completed before shutting down |
| IMMEDIATE | Forcibly terminates all currently running operations and shuts down after rolling back all in-progress transactions |
| ABORT | Forcibly terminates the Tibero process |
| ABNORMAL | Forcibly terminates the server process unconditionally without connecting to the Tibero server (recommended for emergency use only) |

{% hint style="warning" %}
**Caution **

When shutting down in ABORT mode, some system resources (shared memory, semaphores, etc.) may not be released, which may require damage recovery. Use only in the following situations:

- When normal shutdown is not possible due to an internal Tibero error
- When a H/W problem occurs and Tibero must be shut down immediately
- When an emergency such as hacking occurs and Tibero must be shut down immediately
{% endhint %}

{% hint style="warning" %}
**Caution**

ABNORMAL mode shuts down the server immediately using an OS forced termination signal, and since system resources (shared memory, semaphores, etc.) are not released, a damage recovery process is required after restart. Use only in the following situations:

- When normal shutdown is not possible due to an internal Tibero error
- When a shutdown command has been issued using a shutdown mode other than ABNORMAL but is delayed, and an immediate forced shutdown is required
- When execution of a shutdown mode other than ABNORMAL fails due to external factors such as H/W or OS issues
- When an emergency such as hacking occurs and Tibero must be shut down immediately
{% endhint %}
{% endtab %}
{% tab title="Tmax OpenSQL" %}
Support is planned for a future release.
{% endtab %}
{% endtabs %}

1. **Click the Restart** button.
