# Feature Usage Guide / Management / Tablespace

**OwlDB**You can manage the logical and physical storage space of databases running in OwlDB. A single tablespace can contain multiple data files. Tablespace inquiry, modification, and deletion are only available when the database status is `Running` . 



# **Tablespace Inquiry**

1. **OwlDB console screen > Management > Tablespace** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose tablespaces you want to view.
3. View the list of tablespaces. You can filter by type. You can search directly by name.

| Item | Description |
| --- | --- |
| Name | Tablespace name |
| Type | Tablespace type <br>• **Permanent** : Stores permanent data; generally the most commonly used type<br>• **Temporary** : Stores temporary data; data is deleted when the session ends or the operation completes<br>• **Undo** : Stores data for modified records |
| Status | Tablespace status<br>• **ONLINE** : The tablespace is properly connected to the database and available for use<br>• **OFFLINE** : The tablespace is disconnected from the database (objects stored in the tablespace are inaccessible) |
| Used/Total Size | • **Used Size** : The total amount of space currently in use by the data files belonging to this tablespace<br>• **Total Size** : The total amount of space allocated to the data files belonging to this tablespace |
| Total/Max Size | • **Total Size** : The total amount of space allocated to the data files belonging to this tablespace<br>• **Max Size** : The total maximum amount of space that can be allocated to the data files belonging to this tablespace |
| Logging | Whether logging is enabled |
| Allocation Type | Extent allocation method <br>• **SYSTEM** : A method that dynamically allocates extent size based on system demand<br>• **UNIFORM **: A method that stores objects using extents of equal size |
| Next Extent | Size of the next allocated extent |



---

# **Creating a Tablespace**

1. **OwlDB console screen > Management > Tablespace** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database in which you want to create a tablespace.
3. **Create** Click the button.

{% hint style="info" %}
**Note**

Based on a data block size of 8KB, even if UNIFORM SIZE is set smaller than 128KB, it will be set to the minimum extent size of 128KB.
{% endhint %}



---

# **Modifying a Tablespace**

1. **OwlDB console screen > Management > Tablespace** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose tablespace you want to modify.
3. **Modify **Click the button.



---

# **Deleting a Tablespace**

1. **OwlDB console screen > Management > Tablespace** Navigate to the menu.
2. **DB Alias** Click the dropdown button to select the database whose tablespace you want to delete.
3. **Delete** Click the button.



---

# **Data File Inquiry**

1. '[Tablespace Inquiry](#undefined)' to select the database whose data files you want to view.
2. **Tablespace** Click the radio button to select the tablespace whose data files you want to view.
3. View the list of data files. You can filter by whether auto extend is enabled. You can search directly by data file name.

| Item | Description |
| --- | --- |
| Tablespace Name | Tablespace name |
| Name | Data file name |
| Online Status | Data file status<br>• **SYSOFF: **system offline file<br>• **SYSTEM: **system online file<br>• **OFFLINE**<br>• **ONLINE**<br>• **RECOVER: **Datafile needs to be recovered<br>• **AVAILABLE** |
| Used/Total Size | • **Used Size** : The amount of space currently in use by the data file<br>• **Total Size** : The amount of space allocated to the data file |
| Total/Max Size | • **Total Size** : The amount of space allocated to the data file<br>• **Max Size** : The maximum amount of space that can be allocated to the data file |
| Auto Extend | Whether auto extend is enabled |
| Next | Next extension size |
| Physical Reads | Number of physical reads |
| Physical Writes | Number of physical writes |
| Single Block Reads | Number of single block reads |



---

# **Creating a data file**

1. '[Viewing data files](#undefined-4)' to select the tablespace in which to create the data file.
2. **Create** Click the button.



---

# **Modifying a data file**

1. '[Viewing data files](#undefined-4)' to select the tablespace containing the data file to modify.
2. **Modify** Click the button.



---

# **Deleting a data file**

1. '[Viewing data files](#undefined-4)' to select the tablespace containing the data file to delete.
2. **Delete** Click the button.
