<H1>zabbix line 通知</H1><BR>
<BR>
用途：如果監控的目標有狀況會用LINE通知<BR>


腳本內容：
#!/usr/bin/bash
# LINE Notify Token - Media > "Send to".
TOKEN="jZMEHc1QxgkqSp9hwvmXocoRhMO0UVkls7bpxoUeyV1"
# {ALERT.SUBJECT}
subject="$1"
# {ALERT.MESSAGE}
message="$2"
curl https://notify-api.line.me/api/notify -H "Authorization: Bearer ${TOKEN}" -d "message=${message}"






[參考資料](https://dotblogs.com.tw/xerion30476/2019/08/28/153643)
