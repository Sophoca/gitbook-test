# Database Server Common Prerequisites

This is the common preparation procedure for database servers monitored by OwlDB. For other procedures depending on configuration method, such as disk requirements, network settings, and deployment file configuration, refer to the [Installation DB Environment Preparation Guide](db.md)and [Registration DB Environment Preparation Guide](db-1.md)respectively.

## Timezone Configuration

Configure the Timezone of the database server correctly. For multi-node configurations such as TAC and DR, **the Timezone must be identical across all nodes.**If Timezones differ, data consistency issues and log timestamp mismatches may occur.

```bash
# Check current Timezone
timedatectl

# Set Timezone (e.g., Asia/Seoul)
sudo timedatectl set-timezone Asia/Seoul

# Verify configuration
timedatectl
```

## OS User / SSH Key Configuration

{% hint style="info" %}
**Note**

This section is required** only when using DR configuration.**[T_17] In a DR configuration, OwlDB transfers data files between nodes via SCP. To enable this, a dedicated OS user is created on each node, and a shared key pair is distributed to allow passwordless SSH access.
{% endhint %}

DR 구성에서는 OwlDB가 노드 간 SCP를 통해 데이터 파일을 전송합니다. 이를 위해 각 노드에 전용 OS 사용자를 생성하고, 패스워드 없이 SSH 접속이 가능하도록 공용 키페어를 배포합니다.

The example values used in the following procedures are listed below. Please substitute them with values appropriate for your actual environment.

- DB OS user: `tibero`
- SSH port: `22`
- Database nodes: Node1 (Primary): `10.10.0.11` Node2 (Standby): `10.10.0.12` Node3 (Standby): `10.10.0.13`
- Cluster internal network CIDR: `10.10.0.0/16`

### 1. Create a Dedicated DB OS User

Create users with **the same UID/GID**on all nodes.

```bash
# Run as root on each node
groupadd -g 1100 dba
useradd  -u 1100 -g dba -m -s /bin/bash tibero
```

{% hint style="warning" %}
**Caution**

If UID/GID differs between nodes, ownership of files transferred via SCP will be mismatched, preventing the DB process from reading those files. Specify identical numeric values explicitly when creating the user.
{% endhint %}

### 2. Generate SSH Key Pair (Performed once on Node 1 only)

Generate a key pair exactly once on Node1 (`10.10.0.11`). **This key pair will serve as the shared key for all nodes.**

```bash
# Run as tibero account on node1
su - tibero
mkdir -p ~/.ssh && chmod 700 ~/.ssh
ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519 -C "owldb-shared-key"
```

| Option | Description |
| --- | --- |
| `-t ed25519` | Recommended algorithm. When using RSA: `-t rsa -b 4096` |
| `-N ""` | No passphrase for automated SCP |
| `-C` | Comment for key identification |

{% hint style="warning" %}
**Caution**

The private key must also be distributed to all nodes. Since every node must perform SCP to every other node (node1 → {node2, node3}, node2 → {node1, node3}, …), **all nodes act as SSH clients as well.** The private key must exist locally on the SSH client side in order to sign the challenge.
{% endhint %}

### 3. Configure authorized_keys

Register the generated public key in `authorized_keys`.

```bash
# Run as tibero account on node1
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

### 4. Distribute the Key Set

On each Standby node, retrieve node1's key files via SCP.

```bash
# Run as tibero account on each Standby node (node2, node3)
mkdir -p ~/.ssh && chmod 700 ~/.ssh

scp -P 22 tibero@10.10.0.11:~/.ssh/id_ed25519      ~/.ssh/id_ed25519      # private key
scp -P 22 tibero@10.10.0.11:~/.ssh/id_ed25519.pub  ~/.ssh/id_ed25519.pub  # public key

cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519 ~/.ssh/authorized_keys
```

After distribution is complete, verify the permission status of `~/.ssh/` on all nodes.

```
drwx------   tibero:dba  ~/.ssh
-rw-------   tibero:dba  ~/.ssh/id_ed25519
-rw-r--r--   tibero:dba  ~/.ssh/id_ed25519.pub
-rw-------   tibero:dba  ~/.ssh/authorized_keys
```

### 5. Pre-register known_hosts

To prevent host key prompts from appearing when automated scripts run, collect the host public keys of all cluster nodes on each node in advance.

```bash
# Run as tibero account on each node
ssh-keyscan -p 22 -t ed25519 10.10.0.11 10.10.0.12 10.10.0.13 > ~/.ssh/known_hosts
chmod 644 ~/.ssh/known_hosts
```

### 6. **Harden sshd Configuration and Restrict Source IP**

Apply the following sshd settings to enhance security.

The following consolidates **required items**for the SSH public key authentication described in this manual to function correctly, along with **recommended items**for security hardening. Apply identically on all nodes.

**1) Configuration Items**

| Item | Recommended value | Category | Description |
| --- | --- | --- | --- |
| `PubkeyAuthentication` | `yes` | **Required** | Allows public key-based authentication. This is the authentication method used in this manual and must be enabled. |
| `AuthorizedKeysFile` | `.ssh/authorized_keys` | **Required** | Path to the per-user public key list file. This is the sshd default; if it has been changed, the file location used in steps 3 and 3.4 must be updated accordingly. |
| `StrictModes` | `yes` | Recommended | sshd verifies the permissions of the user's home directory and key files. If permissions are too permissive, authentication will be denied. This is why the permission values specified in step 3.4 must be strictly observed. |
| `PermitRootLogin` | `no` | Recommended | Blocks SSH access by the root account to reduce the attack surface. |
| `PasswordAuthentication` | `no` | Recommended | Blocks password-based authentication, allowing only public key authentication. This prevents brute-force attacks. |
| `AllowUsers` | `tibero` | Recommended | Allow SSH access only for the DB-dedicated OS user to block access from other accounts. |

**2) How to apply (if necessary)**

`/etc/ssh/sshd_config` Or `/etc/ssh/sshd_config.d/` Edit the relevant entry under the file, then reload sshd to apply the changes.

```
# Recommended configuration example for /etc/ssh/sshd_config
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
StrictModes yes
PermitRootLogin no
PasswordAuthentication no
AllowUsers tibero
```

```bash
# Reload configuration (re-reads settings without restarting the sshd process)
systemctl reload sshd      # RHEL/CentOS/Rocky family  
# systemctl reload ssh       # Ubuntu/Debian family

# Apply verification — if Active: active (running), reload was successful
systemctl status sshd      
# systemctl status ssh
```

{% hint style="warning" %}
**Caution**

When changing sshd configuration from a remote SSH session, if sshd fails to reload due to an incorrect setting, additional SSH connections may be refused. Ensure you have a separate console access method available before proceeding. 

Immediately after applying the change, it is strongly recommended to verify that sshd is operating normally using the `systemctl status` command.
(`Active: failed` If an error message is displayed, revert the configuration immediately.)
{% endhint %}

** 3) Source IP restriction**

`authorized_keys` Prepend the `from=` option to the entry to restrict key validity to the cluster's internal network only.

```
from="10.10.0.0/16,127.0.0.1" ssh-ed25519 AAAA... owldb-shared-key
```

{% hint style="warning" %}
**Caution**

This key must be used exclusively by the DB-dedicated OS user (`tibero`). `**root**`** Never share this as the SSH key for the account publicly.
**Ensure data directory ownership is organized in advance so that recovery tasks and SCP do not require root privileges.
{% endhint %}
