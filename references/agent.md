# Precautions When Restarting Agent

`agent.env` If a value change is required or the Agent fails to start for an unknown reason, you can restart the Agent with the following command.

bash

```bash
sh tbagent_start.sh
```

When restarting, the following selection prompt is displayed.

```
============================================
  DB Agent config.json generation script
============================================
▲ Warning: config.json file already exists.
  1) Overwrite the existing config.json and continue
     ▲ Warning: If you perform this operation on a host that is properly installed/registered, the Agent will start with the new config.json,
             and OwlDB will no longer be able to identify that host.
  2) Use the existing config.json as-is and continue
  3) Cancel
```

| Situation | Selection |
| --- | --- |
| Restarting on a host that is properly installed/registered in OwlDB | You must select **option 2** Selection |
| Restarting on a host that has not yet been registered in OwlDB | Either option 1 or 2 is acceptable |

{% hint style="warning" %}
**Caution**

If you select option 1 on a properly registered host, `config.json`a new config.json will be generated and the Agent's unique identifier will change. In this case, OwlDB will no longer be able to identify that host.
{% endhint %}
