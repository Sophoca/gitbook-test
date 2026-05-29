# Jobs

**Management > Overview** or **Dashboard**after selecting a database from **[Action]** button to perform the following functions.

### **Stop and Start Database**

**[Stop]** button to temporarily stop the database. A stopped database can be restarted by clicking the **[Start]** button.



---

### **Delete Database**

This feature is only available for installed databases.

1. **[Delete]** Click the button.
2. Enter the database alias in the input field.
3. **[OK]** Click the button.

{% hint style="warning" %}
**Caution**

A deleted database cannot be recovered, and all data will be permanently deleted.
{% endhint %}



---

### **Deregister**

A registered database can be excluded from OwlDB management by deregistering it rather than deleting it.
Even after deregistration, the actual database remains in the operating environment and can be re-registered if needed.

1. **[Deregister]** Click the button.
2. Enter the database alias in the input field.
3. **[OK]** Click the button.



---

### [**Role Switchover**](#switchover)** (Switchover)**

This feature is activated when a DR configuration is set up.

1. **[Role Switchover]** Click the button.
2. Enter the password and click the **[OK]** button.
3. Select the Standby database to become the new Primary and enter the reason for the change.
4. **[OK]** Click the button.

{% hint style="info" %}
**Note**
The dropdown list displays only Standby databases with a status of `Available`.
{% endhint %}



---

### [**Failback**](#failback)

This feature is activated only when a TAC-DR configuration is set up. 

1. **[Failback]** Click the button.
2. Enter the password and click the **[OK]** button.
