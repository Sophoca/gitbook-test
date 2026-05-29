# Backup/Recovery

Backup and recovery features are provided to minimize data loss and ensure business continuity. By leveraging the Recovery Manager (RMGR) within Tibero, data at a specific point in time can be safely preserved and restored when needed.

Two types of backups are supported: Full backup and Incremental backup.
Full backup backs up the entire database, while Incremental backup backs up only the data that has changed since the most recent backup. The retention period for backups can be set from a minimum of 1 hour to a maximum of 365 days. For long-term retention, a Full backup can be selected for permanent storage with unlimited retention.
Recovery restores the database to a specific point in time based on backed-up or archived data.

The available database operational states for each operation are as follows.

| Operation | Available operational states |
| --- | --- |
| Backup creation | `Running` |
| Recovery | `Running`, `Down`, `Degraded` |
| Backup deletion | No restriction |

{% hint style="info" %}
**Note**

Database operational states

- `Running` : Normal operation
- `Down` : Database stopped state
- `Degraded` : State in which a failure has occurred on some nodes
{% endhint %}

{% hint style="warning" %}
**Caution**

If files within the archive log storage path are **arbitrarily modified or deleted, the recovery feature may not function correctly**.
{% endhint %}

---

## Backup storage usage

The total usage of the backup disk can be checked at a glance.

| Item | Description |
| --- | --- |
| Total storage | Total capacity of the backup disk (unit: GB) |
| Backup | Capacity of Full / Incremental backups |
| Archive Log | Capacity of archive log backups |
| Safety Margin | Available free capacity |

1. **OwlDB console screen > Management > Backup/Recovery > Backup Scheduler** or** Backup **Navigate to the menu.
2. Storage usage is displayed at the top.

## **Automatic backup settings**

| Item | Description | Interval | Retention period |
| --- | --- | --- | --- |
| Full backup | Automatically creates a Full backup by setting an interval | 1 hour ~ 7 days | • 1 hour ~ 365 days<br>• Permanent retention |
| Incremental backup | Automatically creates an Incremental backup by setting an interval | 1 hour ~ 7 days |   |

1. **OwlDB console screen > Management > Backup/Recovery > Backup Scheduler** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database for which automatic backup will be configured.
3. **Edit** Click the button.



---

## **Backup management**

| Item | Description | Retention period |
| --- | --- | --- |
| Backup | • Safely preserves data at a specific point in time<br>• Divided into Full/Incremental backup | • 1 hour ~ 365 days<br>• Permanent retention |

## ** Backup creation**

1. **OwlDB console screen > Management > Backup/Recovery > Backup** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database for which a backup will be created.
3. **Create** Click the button.
4. Select either Full or Incremental, enter a name and retention period, then click the **Create** button.



## **Backup deletion**

1. **OwlDB console screen > Management > Backup/Recovery > Backup **Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database from which a backup will be deleted.
3. :2611: Click the icon to select the Full backup to delete.
4. **Delete** Click the button.

{% hint style="warning" %}
**Caution**

Deleted backups cannot be recovered, and all data will be permanently deleted. 

When deleting a backup, subordinate Incremental backups are deleted together. Deleting an individual Incremental backup is not supported.
{% endhint %}

## 

## **Backup Recovery**

1. **OwlDB console screen > Management > Backup/Recovery > Backup** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database to recover.
3. :2611: Click the icon to select the backup to recover.
4. **Recovery** Click the button.

{% tabs %}
{% tab title="Full Restore" %}
4-1. **Full Restore** Click the button to select the recovery type.

{% hint style="warning" %}
**Caution**

Performing a Full Restore to the selected backup point will change the backup chain, and backups created after that point will be deleted.
{% endhint %}
{% endtab %}
{% tab title="PITR" %}
4-1. **PITR **Click the button to select the recovery type.

4-2. Enter the recovery date and time.

{% hint style="warning" %}
**Caution**

All currently stored backups will be deleted when performing point-in-time recovery.
{% endhint %}
{% endtab %}
{% endtabs %}

1. **Recovery** Click the button.
2. You can check the progress result in 'Recovery History'.



## Edit Backup

1. **OwlDB console screen > Management > Backup/Recovery > Backup **Navigate to the menu.
2. Click the DB Alias dropdown button to select the database whose backup you want to edit.
3. :2611: Click the icon to select the backup to edit.
4. **Edit **Click the button.
5. Edit the name and retention period, then **Save** Click the button.

{% hint style="info" %}
**Note**

The retention period of an Incremental backup follows the Full Backup policy and cannot be modified separately.
{% endhint %}

---

## **Recovery History**

1. **OwlDB console screen > Management > Backup/Recovery > Recovery History** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose recovery history you want to view.
3. View the backup recovery history. You can filter by search period and status. You can search directly by name, creation date, and expiration date to view the recovery history.
