# Installation Guide / OwlDB Connection Verification

## 1. Verifying Agent Connection

Access the OwlDB UI, then click the navigation button to verify the Agent connection status.

```
http://[OwlDB 서버 IP]:[UI_PORT]/owldb/#/auth/login
```

## 2. Verifying UID/GID Match (When Configuring DR)

Run the following command on each node to verify that the UID/GID values, **including the numeric values, are identical** by comparing them.

```bash
# 각 노드에서 실행
id tibero
```

Expected result (identical across all nodes):

```
uid=1100(tibero) gid=1100(dba) groups=1100(dba)
```

If the UID or GID numeric values differ, recreate the user on the affected node by following the OS user creation procedure in the database server common prerequisites.

## 3. Verifying SSH Key Authentication (When Configuring DR)

From each node, attempt SSH connections to all other nodes using the tibero account and verify that **the connection is established without a password.** Verify that the connection succeeds.

```bash
# Node1(10.10.0.11)에서 tibero 계정으로 실행
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.12
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.13

# Node2(10.10.0.12)에서 tibero 계정으로 실행
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.11
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.13

# Node3(10.10.0.13)에서 tibero 계정으로 실행
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.11
ssh -p 22 -i ~/.ssh/id_ed25519 -o BatchMode=yes tibero@10.10.0.12
```

`BatchMode=yes`forces an immediate failure if a password prompt occurs, making it possible to clearly detect key authentication failures.

## 4. Verifying Key File Consistency (When Configuring DR)

Verify using hashes that the deployed key files are identical across all nodes.

```bash
# 각 노드에서 tibero 계정으로 실행 후 결과 비교 (모든 노드 동일해야 함)
sha256sum ~/.ssh/id_ed25519
sha256sum ~/.ssh/id_ed25519.pub
```

If the hashes differ between nodes, redo the [key set distribution step](#id-4)described in the database server common prerequisites.
