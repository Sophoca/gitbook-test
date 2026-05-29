# Database Exploration

On the OwlDB screen, **[Discover]** clicking the button automatically collects configuration information from the customer infrastructure where the OwlDB Agent is installed, allowing you to check the current status on the dashboard.

**Please verify the following before running a discovery.**

- Discovery and its sub-features (registration, change detection) are available to administrator accounts only.

## Discovery Process

1. **OwlDB console screen** > **Dashboard**Navigate to.
2. Click the Discover button.
3. Discovery results are displayed across four categories. For details on each category, refer to the **Discovery Results** section below.
4. Review the results and proceed with the appropriate follow-up action for each category.

{% hint style="info" %}
**Note**

The database discovery feature is available only from the Root account.
{% endhint %}

---

## Discovery Results 

### **Installable Host Lookup**

You can view a list of hosts on which a database can be installed. Each host's **Hostname, CPU, Memory, and OS information**is also provided. The installable host category is read-only and requires no additional follow-up action.

---

### **Registerable Databases**

Databases already running in the customer environment are automatically discovered and presented as a list. Select the desired database from the list and click the **[Register]** button to proceed with the registration process.

---

### Change Detection

If a database registered in OwlDB is modified directly outside of OwlDB, the changes are detected and reported.

Change detection identifies the following two types of changes.

| Type | Description | Example | Follow-up Action |
| --- | --- | --- | --- |
| **Spec Change** | When the configuration information of a database has changed | Increase/decrease in node count | **[Spec Change]** Click the button to apply the detected changes |
| **Status Change** | When the role of a node in a DR configuration has changed | Primary ↔ Standby role switchover | **[Status Change]** Click the button to apply the detected changes |

{% hint style="info" %}
**Note**

**Databases installed through OwlDB are excluded from change detection.**

If a spec change and a status change are detected simultaneously, the status change is processed first. In the status change modal, clicking the **[Go to Spec Change]** button navigates to the spec change page after the status change has been applied.
{% endhint %}

---

### Abnormal Nodes

Nodes for which OwlDB was unable to properly retrieve configuration information during discovery are marked as abnormal nodes.

Abnormal nodes occur in the following two cases.

| Case | Description |
| --- | --- |
| When DB configuration cannot be determined at all | The affected node is marked as a single abnormal node |
| When DB configuration is only partially determined | The identified nodes are grouped and displayed as a single abnormal node |

If an abnormal node occurs, refer to the separate handling guide and take the appropriate action.
