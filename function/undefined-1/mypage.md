# Account Roles Guide

## Root

The Root account can create, view, and modify Member accounts, and can grant or revoke access permissions to specific DB services. It can also use database installation, registration, and infrastructure discovery features.

When a Member requests account creation, the request is forwarded to Root, and once Root approves it, the Member account is activated.



## Member

Members can use the operation and management features provided by OwlDB (monitoring, backup/recovery, parameter management, etc.) only for DB services to which access has been granted by Root. Members can also directly request Root to create their own account.



## Permission Matrix by Role

| Feature Category | Detailed Feature | Root | Member |
| --- | --- | --- | --- |
| Account Management | User Creation and Deletion | O | X |
| Permission Management | DB Service Assignment | O | X |
| Service Management | Service Creation (Installation/Registration) and Deletion | O | X |
| DB Management | • Spec Change<br>• Tablespace Management<br>• Parameter Management<br>• Backup/Recovery<br>• Monitoring | O | O |

---
