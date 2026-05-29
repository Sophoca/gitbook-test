# Reference / Precautions When Restarting Agent

`agent.env` If a value change is required or the Agent fails to start for an unknown reason, you can restart the Agent using the command below.

bash

```bash
sh tbagent_start.sh
```

When restarting, the following selection prompt is displayed.

```
============================================
  DB Agent config.json 생성 스크립트
============================================
▲ 경고: config.json 파일이 이미 존재합니다.
  1) 기존 config.json을 덮어쓰고 계속 진행
     ▲ 경고: 정상 설치/등록된 호스트에서 이 작업을 수행하면 새로운 config.json으로
             Agent가 기동되어, OwlDB에서 해당 호스트를 더 이상 식별할 수 없게 됩니다.
  2) 기존 config.json을 그대로 사용하고 계속 진행
  3) 취소
```

| Situation | Selection |
| --- | --- |
| Restarting from a host that is normally installed/registered in OwlDB | Must select **2** Select |
| Restarting from a host that has not yet been registered in OwlDB | Either 1 or 2 is acceptable |

{% hint style="warning" %}
**Caution**

If you select 1 from a normally registered host, `config.json`a new one will be created, changing the Agent's unique identifier. In this case, the corresponding host can no longer be identified from OwlDB.
{% endhint %}
