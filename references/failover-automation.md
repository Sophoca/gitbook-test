# Reference / Disaster Recovery (DR)

OwlDB provides disaster recovery (DR) functionality to prepare for situations where database services are interrupted due to unexpected disasters or failures. Through DR configuration, data loss can be minimized and services can be quickly restored in the event of a failure.

---

## DR Configuration Methods

You can use OwlDB's disaster recovery functionality by selecting DR during database installation or by registering a database in a DR configuration. Along with whether to use DR, you also configure the 
**Failover Automation Level**, which determines how far the system will automatically respond in the event of a failure.** **The failover automation level ranges from Level 0 (manual) to Level 3 (full automation), and you can select the level that matches your operating environment and requirements.

### **Failover Automation Levels**

{% hint style="danger" %}
**The automation levels supported in OwlDB v1.3 vary by topology and are as follows. **

- **Single-DR: supports Level 0, Level 1, Level 3**
- **TAC-DR: supports Level 0, Level 1**
{% endhint %}

| Level | Name | Description |
| --- | --- | --- |
| Level 0 | Manual | In the event of a failure, the user must manually promote the Standby to Primary. |
| Level 1 | Auto Failover | In the event of a failure, the system automatically switches the Standby to Primary. Recovery and resource optimization must be performed manually. |
| Level 2 | Auto Rebuild | After automatic failover, a new Standby is automatically created to restore the original configuration. |
| Level 3 | Full Automation | After failover, the entire process including recovery and unused resources is handled automatically. Because recovery speed is the top priority, some recent data may be lost. |

---

## Failover Features

OwlDB provides the following failover features to respond to failures in a DR configuration.

### **Failover**

When a failure occurs in the Primary database, this is the operation of promoting the Standby to a new Primary to continue service. Failover consists of two phases.

- **Standby Promotion** — Promotes the Standby to Primary to ensure service continuity. Once promotion is complete, the new Primary DB is immediately available.
- **Configuration Normalization** — An operation to restore the original high-availability configuration, performed sequentially after Standby promotion is complete.

{% hint style="info" %}
The scope of **Failover **execution differs depending on the automation level.

- **Level 1** : Only Standby promotion is performed automatically; configuration normalization must be done manually.
- **Level 3** : Everything from Standby promotion through configuration normalization is performed automatically.
{% endhint %}

### **Failback**

This is the operation of reverting to the original Primary/Standby configuration after a Failover. It can be performed once Failover is complete, and is only supported in TAC-DR configurations.

### **Switchover**

When both Primary and Standby are in a normal state, this is the operation of swapping the two roles. It is used when roles need to be changed as required, or when reverting to the original configuration after the former Primary has been restored as a Standby following a Failover.

---

## Detailed Scenarios by Automation Level

The scenarios below are organized by topology and automation level. Please refer to the scenario that matches your operating environment when performing DR operations.

### Level 0 — Manual

There are no operations handled automatically in the event of a failure. The user performs failover operations directly. 

{% tabs %}
{% tab title="Single - DR" %}
**Manual Response Actions**

When a failure occurs on the Primary, **click the Overview > [Actions] > [Role Switch] **button to promote the Standby to a new Primary. The former Primary transitions to `Retired` status.

**Restoring the Original Configuration**

After completing manual actions, perform the following steps in order to restore the original Primary/Standby configuration.

| # | Level | Action |
| --- | --- | --- |
| 1 | **Standby Reboot** | **In Overview > Instances,**select the Primary instance and click the Restart button. |
| 2 | **Switchover** | **Click the Overview > [Actions] > [Role Switch] **button. |
{% endtab %}
{% tab title="TAC - DR" %}
**Manual Response Actions**

When all nodes in the Primary Cluster fail, the system automatically promotes the Standby to a new Primary. All nodes in the former Primary Cluster transition to `Retired` status.

**Restoring the Original Configuration**

After completing manual actions, to restore the original Primary/Standby configuration, **click the Overview > [Actions] > [Failback]** button.
{% endtab %}
{% endtabs %}

---

### Level 1 — Auto Failover

{% tabs %}
{% tab title="Single - DR" %}
**Automatic Response Actions**

When a failure occurs on the Primary, the system automatically promotes the Standby to a new Primary. The former Primary transitions to `Retired` status.

---

**Restoring the Original Configuration**

After automatic actions are complete, perform the following steps in order to restore the original Primary/Standby configuration.

| # | Step | Action |
| --- | --- | --- |
| 1 | **Standby Reboot** | **Overview > Instances**Select the Primary instance and click the Restart button |
| 2 | **Switchover** | **Overview > [Actions] > [Role Switch] **Click the button |
{% endtab %}
{% tab title="TAC - DR" %}
**Automatic Remediation Actions**

If all nodes in the Primary Cluster fail, the system automatically promotes the Standby to a new Primary. The existing Primary Cluster is changed to the `Retired` state.

---

**Restoring the Original Configuration**

After automatic remediation is complete, to restore the original Primary/Standby configuration, **Overview > [Actions] > [Failback]** Click the button.
{% endtab %}
{% endtabs %}

---

### Step 3 — Full Automation

{% tabs %}
{% tab title="Single - DR" %}
**Automatic Remediation Actions**

If the Primary fails, the system automatically promotes the Standby to a new Primary. The existing Primary is changed to the `Retired` state. Configuration normalization is then performed. 

---

**Restoring the Original Configuration**

Perform the following based on the automatic remediation result.

| Situation | Action | Path |
| --- | --- | --- |
| When only Standby promotion is complete | 1. Standby Reboot | **Overview > Instances**Select the instance and click the Restart button |
|   | 1. Switchover | **Overview > [Actions] > [Role Switch] button click** |
| When configuration normalization is also complete | Switchover | **Overview > [Actions] > [Role Switch] button click** |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If manual operations do not complete successfully, please contact the TmaxTibero customer support team.
{% endhint %}
