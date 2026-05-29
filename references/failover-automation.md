# Disaster Recovery (DR)

OwlDB provides disaster recovery (DR) functionality to prepare for situations where database services are interrupted due to unexpected disasters or failures. Through DR configuration, data loss can be minimized and services can be quickly restored when a failure occurs.

---

## DR Configuration Methods

The disaster recovery feature of OwlDB can be used by selecting DR during database installation or by registering a database in the DR configuration. Along with whether to use DR, the 
**Failover Automation Level**, which determines how far the system will automatically respond in the event of a failure,** **is configured together. The failover level ranges from Level 0 (manual) to Level 3 (fully automated), and you can select the level that suits your operating environment and requirements.

### **Failover Automation Levels**

{% hint style="danger" %}
**The automation levels supported in OwlDB v1.3 vary by topology and are as follows. **

- **Single-DR: Supports Level 0, Level 1, and Level 3**
- **TAC-DR: Supports Level 0 and Level 1**
{% endhint %}

| Level | Name | Description |
| --- | --- | --- |
| Level 0 | Manual | When a failure occurs, the user must manually promote the Standby to Primary. |
| Level 1 | Auto Failover | When a failure occurs, the system automatically switches the Standby to Primary. Recovery and resource optimization must be performed manually. |
| Level 2 | Auto Rebuild | After automatic failover, a new Standby is automatically created to restore the original configuration. |
| Level 3 | Full Automation | All processes after failover, including recovery and unused resources, are handled automatically. Since recovery speed is the top priority, some recent data may be lost. |

---

## Failover Features

OwlDB provides the following failover features to respond to failures in a DR configuration.

### **Failover**

When a failure occurs in the Primary database, this is the operation of promoting the Standby to the new Primary to continue service. Failover consists of two phases.

- **Standby Promotion** — The Standby is promoted to Primary to ensure service continuity. Once promotion is complete, the new Primary DB can be used immediately.
- **Configuration Normalization** — This is an operation to restore the original high-availability configuration, performed sequentially after Standby promotion is complete.

{% hint style="info" %}
The scope of **Failover** execution differs depending on the automation level.

- **Level 1** : Only Standby promotion is performed automatically; configuration normalization must be performed manually.
- **Level 3** : Everything from Standby promotion to configuration normalization is performed automatically.
{% endhint %}

### **Failback**

This is the operation of reverting to the original Primary/Standby configuration after a Failover. It can be performed when Failover is complete, and is only supported in TAC-DR configurations.

### **Switchover**

When both Primary and Standby are in a normal state, this is the operation of switching the two roles with each other. It is used when changing roles as needed, or when reverting to the original configuration after recovering the former Primary as a Standby following a Failover.

---

## Detailed Scenarios by Automation Level

The scenarios below are categorized by topology and automation level. Please refer to the scenario that matches your operating environment when performing DR operations.

### Level 0 — Manual

There are no operations that are automatically handled when a failure occurs. The user directly uses the failover features. 

{% tabs %}
{% tab title="Single - DR" %}
**Manual Action Steps**

When a failure occurs on the Primary, **click the Overview > [Actions] > [Role Switch] **button to promote the Standby to the new Primary. The existing Primary changes to `Retired` state.

**Restoring the Original Configuration**

After completing the manual action, to restore the original Primary/Standby configuration, perform the steps in the following order.

| # | Step | Action |
| --- | --- | --- |
| 1 | **Standby Reboot** | **Select the Primary instance from Overview > Instances and click the Restart button**Select the Primary instance from Overview > Instances, then click the Restart button |
| 2 | **Switchover** | **Click Overview > [Actions] > [Role Switch] **button |
{% endtab %}
{% tab title="TAC - DR" %}
**Manual Action Steps**

When all nodes in the Primary Cluster fail, the system automatically promotes the Standby to the new Primary. All nodes in the existing Primary Cluster change to `Retired` state.

**Restoring the Original Configuration**

After completing the manual action, to restore the original Primary/Standby configuration, **click the Overview > [Actions] > [Failback]** button.
{% endtab %}
{% endtabs %}

---

### Level 1 — Auto Failover

{% tabs %}
{% tab title="Single - DR" %}
**Automatic Action Steps**

When a failure occurs on the Primary, the system automatically promotes the Standby to the new Primary. The existing Primary changes to `Retired` is changed to the status.

---

**Restoring the Original Configuration**

To restore the original Primary/Standby configuration after the automatic action is complete, perform the steps in the following order.

| # | Step | Action |
| --- | --- | --- |
| 1 | **Standby Reboot** | **Overview > Instances**Select the Primary instance and click the Restart button. |
| 2 | **Switchover** | **Overview > [Actions] > [Switch Roles] **Click the button. |
{% endtab %}
{% tab title="TAC - DR" %}
**Automatic Action Tasks**

If all nodes in the Primary Cluster fail, the system automatically promotes the Standby to the new Primary. The existing Primary Cluster is `Retired` changed to the status.

---

**Restoring the Original Configuration**

To restore the original Primary/Standby configuration after the automatic action is complete, **Overview > [Actions] > [Failback]** click the button.
{% endtab %}
{% endtabs %}

---

### Step 3 — Full Automation

{% tabs %}
{% tab title="Single - DR" %}
**Automatic Action Tasks**

If a failure occurs on the Primary, the system automatically promotes the Standby to the new Primary.
The existing Primary is `Retired` changed to the status. Configuration normalization is then performed. 

---

**Restoring the Original Configuration**

Proceed as follows depending on the result of the automatic action.

| Situation | Action | Path |
| --- | --- | --- |
| If only Standby promotion has been completed | 1. Standby Reboot | **Overview > Instances**Select the instance and click the Restart button. |
|   | 1. Switchover | **Overview > [Actions] > [Switch Roles] button click** |
| If configuration normalization has also been completed | Switchover | **Overview > [Actions] > [Switch Roles] button click** |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the manual action cannot be completed successfully, please contact the TmaxTibero customer support team.
{% endhint %}
