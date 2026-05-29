# OwlDB Connection Verification

## 1. Verifying Agent Connection

Access the OwlDB UI, then click the navigation button to verify the Agent connection status.

```
http://[OwlDB 서버 IP]:[UI_PORT]/owldb/#/auth/login
```

## 2. Verifying UID/GID Match (For DR Configuration)

Run the following command on each node to verify that the UID/GID values, including the **numeric values, are identical.** Compare the results.

```bash
# Run on each node
id tibero
```

Expected result (identical across all nodes):

```
uid=1100(tibero) gid=1100(dba) groups=1100(dba)
```

If the UID or GID numeric values differ, re-create the user on that node by following the OS user creation procedure in the database server common prerequisites.

## 3. Verifying SSH Key Authentication (For DR Configuration)

From each node, attempt SSH connections to all other nodes using the tibero account, and verify that the connections are established **without a password.** Verify that the connection succeeds.

```bash
# Run from Node1 (10.10.0.11) using the tibero account
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.12
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.13

# Run from Node2 (10.10.0.12) using the tibero account
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.11
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.13

# Run from Node3 (10.10.0.13) using the tibero account
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.11
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.12
```

`BatchMode=yes`forces an immediate failure if a password prompt appears, allowing key authentication failures to be clearly detected.

## 4. Verifying Key File Consistency (For DR Configuration)

Verify using hashes that the distributed key files are identical across all nodes.

```bash
# Run on each node using the tibero account, then compare results (must be identical across all nodes)
sha256sum ~/.ssh/id_ed25519
sha256sum ~/.ssh/id_ed25519.pub
```

If the hash values differ between nodes, re-perform the [key set distribution step](#id-4)described in the database server common prerequisites.
