# Installation Guide / Database Server Preparation and Installation / Database Server Common Prerequisites

This is the common preparation procedure for database servers monitored by OwlDB. For other procedures based on configuration method — such as disk requirements, network settings, and deployment file configuration — refer to each of the following: [Database Installation Environment Guide](#kZfdffkPU4c5kvp7Dt93)and [Database Registration Environment Guide](#bDtbN7wl9qGNMMDknJFQ)respectively.



## Timezone Configuration

Configure the Timezone of the database server correctly. For multi-node configurations such as TAC and DR, **the Timezone must be identical across all nodes.**If Timezones differ, data integrity issues and log timestamp inconsistencies may occur.

```bash
# 현재 Timezone 확인
timedatectl

# Timezone 설정 (예: Asia/Seoul)
sudo timedatectl set-timezone Asia/Seoul

# 설정 확인
timedatectl
```

## OS User / SSH Key Configuration

{% hint style="info" %}
**Note**

This section is required** only when using a DR configuration.**[T_14]
In a DR configuration, OwlDB transfers data files between nodes via SCP. To enable this, a dedicated OS user is created on each node, and a shared key pair is distributed to allow SSH access without a password.
{% endhint %}

DR 구성에서는 OwlDB가 노드 간 SCP를 통해 데이터 파일을 전송합니다. 이를 위해 각 노드에 전용 OS 사용자를 생성하고, 패스워드 없이 SSH 접속이 가능하도록 공용 키페어를 배포합니다.

The example values used in the procedures below are as follows. Replace them with values appropriate for your actual environment.

- DB OS user: `tibero`
- SSH port: `22`
- Database nodes: Node1 (Primary): `10.10.0.11` Node2 (Standby): `10.10.0.12` Node3 (Standby): `10.10.0.13`
- Cluster internal network CIDR: `10.10.0.0/16`

### 1. Create a dedicated DB OS user

Create the user on all nodes with **the same UID/GID.**[T_27]
Caution

```bash
# 각 노드에서 root 계정으로 실행
groupadd -g 1100 dba
useradd  -u 1100 -g dba -m -s /bin/bash tibero
```

{% hint style="warning" %}
**주의**

If the UID/GID differs between nodes, the ownership of files transferred via SCP will be mismatched, preventing the DB process from reading those files. Specify the same numeric values explicitly when creating the user.
{% endhint %}

### 2. Generate SSH key pair (perform once on Node 1 only)

Generate the key pair exactly once on Node1 (`10.10.0.11`). **This key pair will serve as the shared key for all nodes.**

```bash
# node1에서 tibero 계정으로 실행
su - tibero
mkdir -p ~/.ssh && chmod 700 ~/.ssh
ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519 -C "owldb-shared-key"
```

| Option | Description |
| --- | --- |
| `-t ed25519` | Recommended algorithm. When using RSA, `-t rsa -b 4096` |
| `-N ""` | No passphrase — required for automated SCP |
| `-C` | Comment for key identification |

{% hint style="warning" %}
**Caution**

The private key must also be distributed to all nodes.
Since all nodes must perform SCP to each other (node1 → {node2, node3}, node2 → {node1, node3}, …), **every node also acts as an SSH client.** The private key must exist locally on the SSH client side in order to sign the challenge.
{% endhint %}

### 3. Configure authorized_keys

Register the generated public key in `authorized_keys`.

```bash
# node1에서 tibero 계정으로 실행
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

### 4. Distribute the key set

On each Standby node, retrieve the key files from node1 via SCP.

```bash
# 각 Standby 노드(node2, node3)에서 tibero 계정으로 실행
mkdir -p ~/.ssh && chmod 700 ~/.ssh

scp -P 22 tibero@10.10.0.11:~/.ssh/id_ed25519      ~/.ssh/id_ed25519      # 개인키
scp -P 22 tibero@10.10.0.11:~/.ssh/id_ed25519.pub  ~/.ssh/id_ed25519.pub  # 공개키

cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519 ~/.ssh/authorized_keys
```

After distribution is complete, verify the permission state of `~/.ssh/` on all nodes.

```
drwx------   tibero:dba  ~/.ssh
-rw-------   tibero:dba  ~/.ssh/id_ed25519
-rw-r--r--   tibero:dba  ~/.ssh/id_ed25519.pub
-rw-------   tibero:dba  ~/.ssh/authorized_keys
```

### 5. Pre-register known_hosts

To prevent host key prompts from appearing when automated scripts run, collect the host public keys of all cluster nodes on each node in advance.

```bash
# 각 노드에서 tibero 계정으로 실행
ssh-keyscan -p 22 -t ed25519 10.10.0.11 10.10.0.12 10.10.0.13 > ~/.ssh/known_hosts
chmod 644 ~/.ssh/known_hosts
```

### 6. **Harden sshd configuration and restrict source IPs**

Apply the following sshd settings to improve security.

This section covers both the **required items**needed for SSH public key authentication described in this manual to function correctly, and the **recommended items**for security hardening. Apply these settings identically on all nodes.

**1) Configuration items**

| Item | Recommended value | Category | Description |
| --- | --- | --- | --- |
| `PubkeyAuthentication` | `yes` | **Required** | Allows public key-based authentication. This is the authentication method used by this manual and must be enabled. |
| `AuthorizedKeysFile` | `.ssh/authorized_keys` | **Required** | Path to the per-user public key list file. This is the sshd default; if it has been changed, the file location used in steps 3 and 3.4 must be updated accordingly. |
| `StrictModes` | `yes` | Recommended | sshd validates the permissions of the user's home directory and key files. If permissions are too loose, authentication will be denied. This is why the permission values specified in step 3.4 must be strictly observed. |
| `PermitRootLogin` | `no` | Recommended | Blocks SSH access for the root account to reduce the attack surface. |
| `PasswordAuthentication` | `no` | Recommended | Disables password-based authentication to allow only public key authentication. This prevents brute-force attacks. |
| `AllowUsers` | `tibero` | Recommended | Restricts SSH access to the dedicated DB OS user only, blocking access from other accounts. |

**2) How to apply (if needed)**

`/etc/ssh/sshd_config` or `/etc/ssh/sshd_config.d/` Edit the relevant item under the appropriate file, then reload sshd to apply the changes.

```
# /etc/ssh/sshd_config 권장 설정 예시
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
StrictModes yes
PermitRootLogin no
PasswordAuthentication no
AllowUsers tibero
```

```bash
# 설정 reload (sshd 프로세스 재시작 없이 설정만 다시 읽음)
systemctl reload sshd      # RHEL/CentOS/Rocky 계열  
# systemctl reload ssh       # Ubuntu/Debian 계열

# 적용 검증 — Active: active (running) 이면 reload 성공
systemctl status sshd      
# systemctl status ssh
```

{% hint style="warning" %}
**Caution**

When changing sshd settings from a remote SSH session, if sshd fails to reload due to an incorrect configuration, further SSH connections may be refused. Make sure to have a separate console access method available before proceeding. 

Immediately after applying changes, it is strongly recommended to verify that sshd is operating normally using the `systemctl status` command.`Active: failed` (If an error message is output, revert the configuration immediately.)
{% endhint %}

** 3) Source IP Restriction**

`authorized_keys` Prepend the `from=` option to the entry to restrict key validity to the cluster's internal network only.

```
from="10.10.0.0/16,127.0.0.1" ssh-ed25519 AAAA... owldb-shared-key
```

{% hint style="warning" %}
**Caution**

This key must be used exclusively by the dedicated DB OS user (`tibero`). `**root**`** Never share this as the SSH key for any common account.
**Pre-arrange ownership of the data directory so that recovery tasks and SCP do not require root privileges.
{% endhint %}
