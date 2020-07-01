<h1>ansible</h1><br>
ansible app1 -m command -a "rpm -e httpd"   移除httpd<br>
<br>
ansible 小於200台機器<br>
ansible app1 -m command -a "rpm -q httpd<br>
查詢是否有安裝httpd套件<br>
ansible app1 -m command -a "rpm -e httpd"<br>
移除httpd套件<br>
ansible app1 -m service -a "name=httpd state=restarted"<br>
重新啟動httpd服務<br>
anbile app1 -m yum -a "name=httpd state=present<br>
ansible使用yum module進行httpd的安裝<br>
ansible app1 -m service -a "name=httpd state=started enabled=yes"<br>
使用service module,啟動httpd並且開機會自動啟動<br>
nsible app1 -m copy -a "src=hi.txt dest=/data/hello.txt backup=yes owner=user group=user mode=600"<br>
０拷貝本地的hi.txt到app1上的/data資料夾下,並改名為hello.txt..設定<br>
<br>
backup,owner=user, group=user, mode=600<br>
ansible myapp -m fetch -a "src=/var/log/dmesg dest=/root"<br>
到myapp包含的主機去找到/var/log/dmesg,拷貝回本地的/root資料夾<br>
<br>
ansible app1 -m file -a "path=/data/hello.txt owner=root group=root mode=666"<br>
修改/data/hello.txt檔案<br>
<br>
<br>
<h1>LINE NOTIFY</h1><br>
<br>
#!/bin/bash<br>
// LINE Notify Token - Media > "Send to".<br>
TOKEN="sY8lj0axrgokqnBEYu9bvods2Ge3xt2kds9qIxBbtAa"<br>
<br>
// {ALERT.SUBJECT}<br>
subject="$1"<br>
<br>
// {ALERT.MESSAGE}<br>
message="$2"<br>
<br>
curl https://notify-api.line.me/api/notify -H "Authorization: Bearer ${TOKEN}" -d "message=${message}"<br>
參考資料:https://notify-bot.line.me/zh_TW/<br>
<br>
<h1>YAML</h1><br>
<br>
Wl-Chuang (http://www.wl-chuang.com/blog/2011/11/06/yaml-tutorial/)<br>
YAML簡介 - Xross Tao<br>
什麼是YAML YAML是YAML Ain’t Markup Language的遞迴縮寫（一種來自Opensource界的奇怪幽默，如果你懂，你就…）。顧名思義，它設計的目的是作為表達、傳遞資料的一種資料描述方<br>
2020/5/6<br>
檔在etc/ansible/hosts<br>
在play-book中 yml  tags 表示組別的概念若有使用到才執行若無則無<br>
- hosts: myapp<br>
  remote_user: root<br>
  tasks:<br>
    - name: change hostname<br>
      hostname: name=centos-{{ http_port }}.example.com<br>
<br>
[參考資料](http://www.wl-chuang.com/blog/2011/11/06/yaml-tutorial/)<br>


