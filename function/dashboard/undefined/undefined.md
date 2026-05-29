# Feature Usage Guide / Dashboard / Database Exploration / Database Change Detection

Change detection is a feature that detects changes made to the database configuration outside of OwlDB and reflects them in OwlDB. 

At the top of the dashboard, **Detect** clicking the button will display any DBs with detected changes on the dashboard.

**Check the following before applying detected changes.**

- Applying change detection is available to administrator accounts only.
- **Registered DB**Change detection is provided only for registered DBs. Installed DBs are excluded from change detection.

---

## Change Type

Change detection is divided into the following two types.

| Type | Description |
| --- | --- |
| Spec Change | When the DB configuration is changed outside of OwlDB (e.g., Primary node Scale In/Out) |
| Status Change | When the DB configuration remains the same but the role of a node changes<br>(e.g., Failover occurs, Primary ↔ Standby role switch) |

{% hint style="info" %}
**Note**

If a status change and a spec change are detected simultaneously, the status change is processed first. 

On the dashboard, the DB is displayed only as a status-changed DB.

Change detection is not supported for topology changes.
{% endhint %}

---

## Spec-Changed DB

If Scale In/Out occurs manually outside of OwlDB, after detection, the dashboard displays **Spec Change** a card view with the button activated.

- Scaled-In instances are not displayed in the card view.
- Scaled-Out instances are added and displayed at the bottom of the corresponding role list.

### **How to Apply**

1. Select the DB with a detected spec change from the dashboard.
2. **Spec Change** Click the button to navigate to the Spec Change page.
3. Review the changed spec information and enter any additional information to apply it to OwlDB.

---

## Status-Changed DB

If a role switch or Failover occurs manually outside of OwlDB, after detection, the dashboard displays **Status Change** a card view with the button activated.

The card view displays the existing state stored in OwlDB as-is, and clicking the Status Change button loads a modal window that compares the state before and after the change.

- Left card view: Previous state (state stored in OwlDB)
- Right card view: Current state detected after detection

{% hint style="info" %}
**Note**

When a status change is detected, only the Health information of the instance is retrieved; detailed information such as CPU, Memory, and active sessions is not displayed.
{% endhint %}

### **How to Apply**

This is divided into two cases: when only a status change is detected, and when a status change and a spec change are detected simultaneously.

**When only a status change is detected**

1. Select the DB with a detected status change from the dashboard.
2. **Status Change** Click the button.
3. Review the state before and after the change in the modal window.
4. **Apply** Clicking the button reflects the status change history in OwlDB.

**When a status change and a spec change are detected simultaneously**

1. Select the DB with a detected status change from the dashboard.
2. **Status Change** Click the button.
3. Review the state before and after the change in the modal window.
4. Select the desired action from the options below. **Apply** : Reflects only the status change in OwlDB and returns to the dashboard. **Go to Spec Change** : After reflecting the status change, navigates to the Spec Change page to apply the spec change as well.
