# Parameters

You can query and manage parameters required for database configuration running in OwlDB. For multi-cluster configurations, management changes are applied in bulk. Parameters can only be modified when the instance status is `Available`. (As an exception, `Unavailable` - When DB is Down / Nomount, `Config Value` value modification is available.)

# **Parameter Query**

1. **OwlDB Console > Management** **> Parameter** > **Settings** Navigate to the menu.
2. **DB Alias, Instance Alias **Click the dropdown button to select the database and instance for which you want to configure parameters.
3. View the parameter list. You can filter by whether a parameter is dynamic. You can search and view by name and parameter value directly.

| Item | Description |
| --- | --- |
| Name | Parameter name |
| Data Type | Parameter data type |
| Default Value | Parameter default value |
| Current Value | The current parameter value set by the user |
| Config Value | The parameter value to be applied on restart (currently applied temporarily) |
| Dynamic Parameter | Whether the parameter is dynamic |



---

# **Parameter Configuration (Modification)**

1. **OwlDB Console > Management > Parameter** > **Settings** Navigate to the menu.
2. **DB Alias, Instance Alias** Click the dropdown button to select the database and instance for which you want to configure parameters.
3. **Edit** Click the button.
4. Modify the parameter value. You can filter by whether a parameter is dynamic. You can search and modify by name and parameter value directly.

{% hint style="info" %}
**Note**

A parameter name highlighted in blue indicates a value currently being modified.
{% endhint %}

1. **Import** Clicking the button allows you to select and apply a template saved in '[Parameter Template](#undefined-2)'.
2. **Save** Click the button.

{% hint style="info" %}
**Note**

When modifying only dynamic parameters, you can choose a save option.

- **Save** Clicking the button applies the modified values immediately without restarting the database.
- **Temporary Save** Clicking the button applies the modifications temporarily. When the database is restarted afterward, the values will be restored to the `Config Value` value.
{% endhint %}

{% hint style="warning" %}
**Caution**

When modifications include static parameters, the database must be restarted to apply the changes. Upon restart, all currently connected sessions will be terminated. It may take several minutes to become active again.
{% endhint %}



---

# **Parameter Template**

1. **OwlDB Console > Management > Parameter > Template** Navigate to the menu.
2. **DB Alias, Instance Alias** Click the dropdown button to select the database and instance for which you want to view parameter templates.
3. View the parameter template list.

| Item | Description |
| --- | --- |
| OLTP | A template designed to handle fast processing speeds and high transaction frequency |
| OLAP | A template optimized for large-scale data analysis and complex queries |

1. Clicking a 'parameter template name' allows you to view the detailed parameter values. You can filter by whether a parameter is dynamic. You can search by name and parameter value directly.
2. **Apply** Click the button to apply the parameter template.

{% hint style="warning" %}
**Caution**

The database must be restarted to apply the modifications. Upon restart, all currently connected sessions will be terminated. It may take several minutes to become active again.
{% endhint %}



---

# **Parameter Modification History**

1. **OwlDB Console > Management > Parameter > Modification History** Navigate to the menu.
2. **DB Alias, Instance Alias** Click the dropdown button to select the database and instance for which you want to view the parameter modification history.
3. View the parameter modification history.
