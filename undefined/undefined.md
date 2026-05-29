# Installation Guide / Installation Introduction

To use OwlDB on-premises, some prerequisites must be prepared in the customer environment.
This page first describes the architecture of OwlDB, then explains what preparation is required for each component.

## System Architecture

OwlDB consists of two types of servers.

| Server | Role | Description |
| --- | --- | --- |
| OwlDB Server | Management Server | • The server on which the OwlDB application runs<br>• Provides the web UI and backend services, and communicates with the Agent on the database server to perform installation and management tasks. |
| Database Server | Managed Server | • The server on which the Tibero database and OwlDB Agent are installed<br>• The Agent receives commands from the OwlDB server and performs database installation and operation locally. |

{% hint style="info" %}
**Note**

The OwlDB server and the database server must be configured in separate, independent environments.
{% endhint %}

### Communication Architecture

The OwlDB server and the database server communicate through the Agent installed on each server.

```
[ 사용자 브라우저 ]
        |  HTTP (UI_PORT)
        v
[ OwlDB 서버 ]
   - OwlDB 백엔드
   - OwlDB 프론트엔드
        |  SERVER_PORT (아웃바운드)
        v
[ 데이터베이스 서버 ]
   - OwlDB Agent (tbagent)
   - Tibero DB
```

The Agent is installed on the database server, receives connections from the OwlDB server, and executes tasks required for Tibero installation, startup, and management locally.



## Database Configuration Method

OwlDB on-premises supports two configurations depending on how the database is used.

- **Installed DB** : A method of installing and managing a new database through OwlDB.
- **Registered DB **: A method of registering an already-running database into OwlDB for management.

| Category | Installed DB | Registered DB |
| --- | --- | --- |
| Target DB | Tibero 7.2.5 | Tibero 7 or later |
| Supported OS | Rocky Linux 9.5 or later | CentOS 7, Rocky Linux 8/9, RHEL-based 7/8/9 |

{% hint style="info" %}
**Note**

Installed DB is installed based on the **latest Tibero binary version provided by OwlDB**.

For detailed support conditions and prerequisites for each configuration method, refer to the [Database Installation Environment Guide](#kZfdffkPU4c5kvp7Dt93)and the [Database Registration Environment Guide](#bDtbN7wl9qGNMMDknJFQ).
{% endhint %}

### Required Patch List

The following patches are required to use the database with OwlDB.

| Patch Name | Patch Description |
| --- | --- |
| FS02PS_318447b | Fix for stdout not closing on tbboot<br>**[Note]** Without this patch, **DB startup** related functionality will not work correctly. |
| FS02PS_339919c | Add switchover immediate option on tbdown<br>**[Note]** Without this patch, **failover**/**switchover** functionality will not work correctly. |

## Installation Flow

This guide proceeds in the order described below. Preparation of the OwlDB server and the database server can be done in parallel; connectivity verification is performed after both are ready.

## Distribution File Structure

Before installation, prepare the following two types of distribution files.

| Distribution File | Target Server | Component |
| --- | --- | --- |
| `owldb-cp-installer-*.tar.gz` | OwlDB Server | • OwlDB backend and frontend Docker images<br>• Installation script |
| `owldb-dp-installer-*.tar.gz` | Database Server | • Tibero installation script<br>• tbagent binary<br>• Infrastructure validation script |
