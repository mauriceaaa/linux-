<h1>安裝zabbix</h1>
<br>
 <br>
Centos 7搭建Zabbix 4.0监控系统-：努力变好-51CTO博客<br>
要想实时地了解服务器的运行状况并且能在出现问题时及时解决，利用监控软件是一个很好的途径。就目前而言，有服务器的地方必然少不了监控系统。现有的监控<br>软件有很多，但是Zabbix可以<br>
<br>
<br>
php_value date.timezone Asia/Taipei 改時區<br>
<br>
在運行zabbix之前，先確保：<br>
systemctl start zabbix-server.service<br>
systemctl enable zabbix-server<br>
systemctl start httpd<br>
systemctl start zabbix-agent<br>
systemctl enable zabbix-agent<br>
<br>
<br>
[參考資料](https://blog.51cto.com/14156658/2460214)<br>
