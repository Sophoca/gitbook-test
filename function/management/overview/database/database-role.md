# Feature Usage Guide / Management / Overview / Database / Jobs

**Management > Overview** or **Dashboard**after selecting a database, **[Actions]** button to perform the following functions.

### **Stop and Start Database**

**[Stop]** button to temporarily stop the database. A stopped database can be **[Start]** button to restart it.



---

### **Delete Database**

This feature is available only for installed databases.

1. **[Delete]** button.
2. Enter the database alias in the input field.
3. **[Confirm]** button.

{% hint style="warning" %}
**Caution**

A deleted database cannot be recovered, and all data will be permanently deleted.
{% endhint %}



---

### **Deregister**

A registered database can be excluded from OwlDB management by deregistering it rather than deleting it. Even after deregistration, the actual database remains intact in the operating environment and can be re-registered if needed.

1. **[Deregister]** button.
2. Enter the database alias in the input field.
3. **[Confirm]** button.



---

### [**Role Switchover**](#switchover)** (Switchover)**

This feature is activated when a DR configuration is in place.

1. **[Role Switchover]** button.
2. Enter the password and click the **[Confirm]** button.
3. Select the Standby database to become the new Primary and enter the reason for the change.
4. **[Confirm]** button.

{% hint style="info" %}
**Note**
Only Standby databases with a status of `Available`are displayed in the dropdown list.
{% endhint %}



---

### [**Failback**](#failback)

This feature is activated only when a TAC-DR configuration is in place. 

1. **[Failback]** button.
2. Enter the password and click the **[Confirm]** button.
