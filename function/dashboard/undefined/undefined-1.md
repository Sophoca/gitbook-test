# Feature Usage Guide / Dashboard / Database Exploration / Abnormal Node Remediation

If the association between database nodes is not correctly identified during the discovery process, the affected node is marked as an abnormal node. This page describes how to resolve abnormal node occurrences.

## Resolution

Manually configure the associations between nodes so that the cluster topology is correctly recognized during discovery.

1. Navigate to the Agent installation path on all associated DB nodes.

```
/home/{username}
```

1. In that path, create the `db_scan.info` file.
2. Enter the same TSC ID in the file content.

```
tsc_id={고유한 숫자 값}
```

1. Repeat the above steps with the same TSC ID on all associated nodes.
2. After completing the configuration, re-run discovery. The associations between nodes will be correctly recognized and the cluster topology will be displayed properly.

**Configuration Example** — Cluster consisting of 4 nodes

```
Node 1의 Agent 설치 경로/db_scan.info → tsc_id=262
Node 2의 Agent 설치 경로/db_scan.info → tsc_id=262
Node 3의 Agent 설치 경로/db_scan.info → tsc_id=262
Node 4의 Agent 설치 경로/db_scan.info → tsc_id=262
```

{% hint style="info" %}
**Note**

Each cluster must use a unique TSC ID.

All nodes belonging to the same database must use the same TSC ID.
{% endhint %}
