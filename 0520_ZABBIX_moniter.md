<H1>zabbix line 通知</H1><BR>
<BR>
用途：如果監控的目標有狀況會用LINE通知<BR>
<BR>
<BR>
腳本內容：<BR>
#!/usr/bin/bash<BR>
# LINE Notify Token - Media > "Send to".<BR>
TOKEN="jZMEHc1QxgkqSp9hwvmXocoRhMO0UVkls7bpxoUeyV1"<BR>
# {ALERT.SUBJECT}<BR>
subject="$1"<BR>
# {ALERT.MESSAGE}<BR>
message="$2"<BR>
curl https://notify-api.line.me/api/notify -H "Authorization: Bearer ${TOKEN}" -d "message=${message}"<BR>
<BR>
<BR><BR>
<BR>
<BR>


[參考資料](https://dotblogs.com.tw/xerion30476/2019/08/28/153643)<BR>
