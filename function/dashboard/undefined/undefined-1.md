# Abnormal Node Remediation

If the relationships between database nodes are not correctly identified during the discovery process, the affected nodes are marked as abnormal nodes. This page provides instructions on how to resolve abnormal node occurrences.

## Resolution

Manually configure the relationships between nodes so that the cluster configuration is correctly recognized during discovery.

1. Navigate to the Agent installation path on all associated DB nodes.

```
/home/{username}
```

1. In that path, create the `db_scan.info` file.
2. Enter the same TSC ID in the file content.

```
tsc_id={unique numeric value}
```

1. Repeat the above steps with the same TSC ID on all associated nodes.
2. After completing the configuration, re-run the discovery process. The relationships between nodes will be correctly recognized and the cluster configuration will be displayed properly.

**Configuration Example** — Cluster consisting of 4 nodes

```
Node 1 Agent installation path/db_scan.info → tsc_id=262
Node 2 Agent installation path/db_scan.info → tsc_id=262
Node 3 Agent installation path/db_scan.info → tsc_id=262
Node 4 Agent installation path/db_scan.info → tsc_id=262
```

{% hint style="info" %}
**Note**

Each cluster must use a unique TSC ID.

All nodes belonging to the same database must use the same TSC ID.
{% endhint %}
