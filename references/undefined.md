# Reference / Abnormal Node Remediation Guide

### Failure to Recognize Relationships Between Nodes

During the database discovery process, there may be cases where the relationships between certain nodes cannot be accurately identified. In this case, proceed with manual configuration using the method below.

1. Navigate to the Agent installation path on all associated DB nodes.
2. On each node, `db_scan.info` create the file.
3. Enter the same TSC ID in the file.

```
tsc_id={고유한 숫자 값}
```

For example, for a TSC cluster consisting of 4 nodes, configure as follows.

```
Node 1의 Agent 경로/db_scan.info → tsc_id=262
Node 2의 Agent 경로/db_scan.info → tsc_id=262
Node 3의 Agent 경로/db_scan.info → tsc_id=262
Node 4의 Agent 경로/db_scan.info → tsc_id=262
```

{% hint style="info" %}
**Note**

- The TSC ID must be a unique value.
- All nodes belonging to the same DB configuration must use the same TSC ID.
- After completing the configuration, retrying the DB scan will allow the cluster configuration to be recognized correctly.
{% endhint %}
