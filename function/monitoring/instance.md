# **View overall instance status summary information**

Check the overall instance health status. ([**View overall status summary information**](#health)** **Note) Hovering the mouse over each status displays a popup showing the list of instances with that status. Hovering the mouse over each status displays a popup showing the list of instances with that status.



---

# **Instance Monitoring**

{% hint style="info" %}
**Note**

You can select multiple databases and instances simultaneously for monitoring.
{% endhint %}

1. **OwlDB console screen > Monitoring > Instance Monitoring** Navigate to the menu.
2. **DB Alias**, **Instance Alias** Click the dropdown button to select the database and instance to monitor.
3. Monitor the instance. Hovering the mouse over a chart allows you to view the database and instance name. Each instance is distinguished by color.

| Metric collection method | Description |
| --- | --- |
| TOTAL | A value that displays the current value as-is |
| DIFF | A value that shows the amount of change during the metric collection interval |

{% tabs %}
{% tab title="Tibero" %}
| Metric | Description | Collection method |
| --- | --- | --- |
| CPU Usage (%) | CPU utilization | TOTAL |
| Memory Usage (%) | Memory utilization | TOTAL |
| Active Session Count (CNT) | Number of active sessions | TOTAL |
| Total Session Count (CNT) | Total number of sessions connected to the DB | TOTAL |
| Logical Reads (CNT) | Number of times data was read from the DB buffer cache | DIFF |
| Physical Reads (CNT) | Number of times data was read from disk | DIFF |
| Buffer Cache Hit (%) | Ratio of Logical Reads to Physical Reads | TOTAL |
| Execute Count (CNT) | Number of SQL statements executed in the DB | DIFF |
| Hard Parse Count (CNT) | Number of times a SQL statement was executed by going through the full parsing process rather than being found and executed from the cache | DIFF |
| Redo Entries (CNT) | Number of REDO records generated in the DB | DIFF |
| Replication Lag (TSN Diff) | TSN number difference between Primary and Standby → integer greater than or equal to 0<br>* Displayed on Standby only. | DIFF |
{% endtab %}
{% tab title="Tmax OpenSQL (On-Premise)" %}
{% hint style="info" %}
**Note**

Tmax OpenSQL currently supports On-Premise environments only.
{% endhint %}

| Item | Description | Collection Method |
| --- | --- | --- |
| CPU Usage(%) | CPU utilization | TOTAL |
| Memory Usage(%) | Memory utilization | TOTAL |
| Active Session Count(CNT) | Number of active sessions | TOTAL |
| Total Session Count(CNT) | Total number of sessions connected to the DB | TOTAL |
| Logical Reads(CNT) | Number of data blocks read from memory | DIFF |
| Physical Reads(CNT) | Number of data blocks read from disk | DIFF |
| Buffer Cache Hit(%) | Buffer cache hit ratio | TOTAL |
| Execute Count(CNT) | Number of SQL statements executed in the DB | DIFF |
| Redo Entries(CNT) | Number of Redo Entries (redo records written to the log buffer) | DIFF |
| Block Read Time(ms) | Time spent reading data file blocks from the backend | DIFF |
| Block Write Time(ms) | Time spent writing data file blocks from the backend | DIFF |
| Total DB Size (GB) | Total size of the database | TOTAL |
| Total Swap Memory(MB) | Total size of Swap Memory | TOTAL |
| Used Swap Memory(MB) | Size of Swap Memory currently in use | TOTAL |
| Free Swap Memory(MB) | Size of available Swap Memory | TOTAL |
| Disk Read Rate(KB) | Average amount of data processed per read request from Disk | TOTAL |
| Disk Write Rate(KB) | Average amount of data processed per write request from Disk | TOTAL |
| WAL Size(MB) | Size of the Write-Ahead Log | TOTAL |
| WAL Rate(MB) | WAL generation rate | DIFF |
| Replication Lag(sec) | Replication lag time reflected in the Replication DB | TOTAL |
| Dead Tuple Count(CNT) | Number of Dead Tuples in the database | TOTAL |
| Live Tuple Count(CNT) | Number of Live Tuples in the database | TOTAL |
| Live/Dead Tuple Rate(%) | Ratio of Dead Tuples to Live Tuples in the database | TOTAL |
| Commits(CNT) | Number of commits occurring per second | DIFF |
| Rollbacks(CNT) | Number of rollbacks occurring per second | DIFF |
| Transactions(CNT) | Number of transactions occurring per second | DIFF |
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Note**

If the instance status is not&nbsp;&nbsp;`Available` , some metrics may be missing.
{% endhint %}



---

# **Auto Refresh**

To support real-time updates on the monitoring screen, an auto refresh feature is provided. You can set the refresh interval by clicking the ⚙️ icon in the upper left corner.
