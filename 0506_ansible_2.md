設定檔在etc/ansible/hosts 在play-book中 yml tags 表示組別的概念若有使用到才執行若無則無<br>
<br>
hosts: myapp remote_user: root tasks:<br>
name: change hostname hostname: name=centos-{{ http_port }}.example.com<br>
未完待續..<br>
<br>
