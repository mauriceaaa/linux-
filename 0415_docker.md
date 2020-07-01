`docker run -it centos echo “hi”`<br>
參數it 指與image互動<br>
d指在背後執行 detach<br>
通常在設定的時候會將tag 設定為定值<br>
因為每次上線他會去線上檢查版本若有最新版會自動下載<br>
容器指執行單一的工作若無工作則容器消滅<br>
docker rm CID<br>
若容器存在時移除不用加-f<br>
docker inspect CID 檢視container內容<br>
docker run -it centos bash<br>
ip addr<br>
 <br>

docker ip<br>
 
<br>
- - name=web 讓這個container 命名為web <br>
–p指定port  1234:80 指本機port 為1234 而容器內port 開80<br>
httpd 指要的服務<br> 
 <br>
 <br>
刪除所有container<br>
docker rm -f $(docker ps -a -q) <br>
<br>
<br>
製作image的方式 <br>
1)下載別人的,然後登入容器後,安裝做設置完後再產生新的image<br>
2) Dockerfile<br>
<br>
遠端同步<br>
可參考<br>
https://blog.gtwang.org/linux/rsync-local-remote-file-synchronization-commands/<br>
https://cloud.tencent.com/developer/article/1043373<br>
https://segmentfault.com/a/1190000018096553<br>

