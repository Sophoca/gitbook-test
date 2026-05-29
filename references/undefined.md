# Abnormal Node Remediation Guide

### Failed to Recognize Relationships Between Nodes

During the database discovery process, there are cases where the relationships between certain nodes cannot be accurately identified. In this case, proceed with manual configuration using the method below.

1. Navigate to the Agent installation path of all related DB nodes.
2. On each node, create the `db_scan.info` file.
3. Enter the same TSC ID in the

```
tsc_id={unique numeric value}
```

For example, for a TSC cluster consisting of 4 nodes, configure as follows.

```
Node 1 Agent path/db_scan.info → tsc_id=262
Node 2 Agent path/db_scan.info → tsc_id=262
Node 3 Agent path/db_scan.info → tsc_id=262
Node 4 Agent path/db_scan.info → tsc_id=262
```

{% hint style="info" %}
**Note**

- The TSC ID must be a unique value.
- All nodes belonging to the same DB configuration must use the same TSC ID.
- After completing the configuration, retrying the DB scan will allow the cluster configuration to be recognized correctly.
{% endhint %}
