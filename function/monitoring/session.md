# Feature Usage Guide / Monitoring / Session Monitoring

{% hint style="info" %}
**Note**

You can simultaneously select and monitor multiple databases and instances.
{% endhint %}

1. **OwlDB console screen > Monitoring > Session Monitoring** Navigate to the menu.
2. **DB Alias**, **Instance Alias** Click the dropdown button to select the database and instance to monitor.
3. Check the session list.

{% tabs %}
{% tab title="Tibero" %}
| Item | Description |
| --- | --- |
| SID | Session ID |
| SERIAL Number | Session serial number |
| AUDSID | Auxiliary serial number of the session |
| USER# | Current user ID |
| USERNAME | Current username |
| IPADDR | IP address the current user is connected from |
| COMMAND | SQL type currently being executed <br>• **1**: SELECT<br>• **2**: INSERT<br>• **3**: UPDATE<br>• **4**: DELETE<br>• **5**: MERGE<br>• **6**: CALL |
| STATUS | Session status <br>• **READY **: Session is ready<br>• **RUNNING **: Session is running<br>• **TX_RECOVERING **: Transaction recovery in progress<br>• **SESS_CLEANUP **: Session resource cleanup in progress<br>• **ASSIGNED **: A thread is assigned to the session but not yet ready<br>• **CLOSING **: Session is closing<br>• **ROLLING_BACK **: Statement-level transaction of the PE slave is being rolled back |
| SCHEMA# | Current schema ID |
| SCHEMANAME | Current schema name |
| TYPE | Session type<br>• **WTHR **: Worker thread<br>• **CTHR **: Control thread<br>• **LGWR **: Log writer process<br>• **CKPT **: Checkpoint process<br>• **LARC **: Log archive<br>• **AGENT **: Sequence process<br>• **MTHR **: Monitoring process<br>• **DBWR **: Data block writer process<br>• **LNW **: Log network writer process |
| SQL_ID | SQL identifier of the SQL statement currently being executed |
| SQL_CHILD_NUMBER | Child number of the SQL statement currently being executed |
| PREV_SQL_ID | ID of the most recently executed SQL statement |
| PREV_CHILD_NUMBER | Child number of the most recently executed SQL statement |
| SQL_ET | Elapsed time (in seconds) since the SQL statement was executed |
| LOGON_TIME | Time at which the session was created |
| STATE | Wait state of the thread<br>• INVALID: Not initialized<br>• NEW: Created<br>• IDLE: Ready to execute<br>• RUNNING: Currently executing<br>• WAITING: Waiting for an internal message<br>• RECV_WAITING: Waiting for a client message<br>• STOP_BY_MTHR: Stopped by MTHR<br>• DEAD: Terminated |
| WLOCK_WAIT | Type of lock the session is waiting for |
| WAIT_EVENT | Type of wait_event the session is waiting for |
| WAIT_TIME | Wait time of the wait_event the session is waiting for |
| PGA_USED_MEM | Amount of PGA memory occupied by the session |
| SQL_TRACE | Whether SQL Trace is enabled for the session |
| PROG_NAME | Client program name |
| CLIENT_PID | Process identifier of the client |
| PID | Identifier of the process to which the session belongs |
| WTHR_ID | Index of the worker thread to which the session belongs |
| OS_THR_ID | Identifier of the thread created by the OS to which the session belongs |
| OSUSER | OS account name of the connected session |
| MACHINE | Host name of the connected session |
| TERMINAL | Terminal (tty) information of the connected session |
| MODULE | Name of the module set by the user in the program executed from the client |
| ACTION | Action name set by the user for the module currently being executed |
| CLIENT_INFO | Client information set by the user |
| CLIENT_IDENTIFIER | Client identifier set by the user |
| PDML_ENABLED | Parallel DML activation mode - Yes / No |
| PDML_STATUS | Parallel DML status<br>• FORCE: State changed to force usage<br>• ENABLED: Activated state<br>• DISABLED: Deactivated state |
| PDDL_STATUS | Parallel DDL status<br>• FORCE<br>• ENABLED<br>• DISABLED |
| PQ_STATUS | Parallel query status<br>• FORCE<br>• ENABLED<br>• DISABLED |
| ROW_WAIT_OBJ_ID | Object ID of the table containing the row specified in ROW_WAIT_ROW# |
| ROW_WAIT_FILE_NO | Identifier of the data file containing the row specified in ROW_WAIT_ROW# |
| ROW_WAIT_BLOCK_NO | Identifier of the block containing the row specified in ROW_WAIT_ROW# |
| ROW_WAIT_ROW_NO | Row currently locked |
| CONSUMER_GROUP | Name of the consumer group to which the current session belongs |
| CONSUMED_CPU_TIME | Cumulative CPU time consumed by the session |

{% hint style="info" %}
**Note**

The LOGON_TIME field displays time based on the database timezone. This may differ from the user's local system time (browser time).
{% endhint %}
{% endtab %}
{% tab title="Tmax OpenSQL (On-Premise)" %}
{% hint style="info" %}
**Note**

Currently, Tmax OpenSQL is only supported in On-Premise environments.
{% endhint %}

| Item | Description |
| --- | --- |
| # | Row number |
| PID | Process identifier |
| IP ADDR | IP address of the connected client |
| LOGON TIME | Time the session was started |
| CLIENT HOSTNAME | Hostname to which the session is connected |
| PREV SQL ID* | ID of the last executed SQL |
| PROGRAM NAME | Name of the client program |
| SCHEMA NAME | Name of the currently used schema |
| SCHEMA NUMBER | ID of the currently used schema |
| SQL ELAPSED TIME | Elapsed Time of the SQL currently being executed in the session |
| SQL ID* | ID of the SQL currently being executed |
| STATUS | Status of the session |
| TYPE | Type of the session |
| USERNAME | Name under which SQL is executed for the session |
| USER ID | ID under which SQL is executed for the session |
| WAIT EVENT | Type of event the session is waiting on |
| LEADER PID | Process ID of the parallel group leader |
| CLIENT PORT | Port number of the client |
| XACT START | Time the current transaction of the process was started |
| STATE CHANGE | Time the state was last changed |
| BACKEND XID | Transaction ID assigned when a query starts |
| BACKEND XMIN | Minimum transaction ID relevant to the current query |
| QUERY | Last executed SQL<br>(If status is active, the SQL currently being executed) |

{% hint style="info" %}
**Note**

*PREV SQL ID and SQL ID may be expressed as negative numbers. These values can be queried from the pg_stat_statements view.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Caution**

If the instance status is not&nbsp;&nbsp;`Available` , some metrics may be missing.
{% endhint %}



---

# **Auto Refresh**

To support real-time updates on the monitoring screen, an auto refresh feature is provided. Click the ⚙️ icon in the upper left to configure the refresh interval. 



---

# **Elapsed Time Alert**

When the configured time threshold is exceeded, the corresponding table row is highlighted to provide a visual alert to the user. Click the ⚙️ icon to configure the threshold.

| Item | Description |
| --- | --- |
| Warning | - Range: 0.1 ~ 1000.0 seconds<br>- Displayed with red highlighting<br>- Set to a longer duration than the Caution level |
| Caution | - Range: 0.1 ~ 999.0 seconds<br>- Displayed with orange highlighting<br>- Set to a shorter duration than the Warning level |
