CentOS 7 自建 SSL 憑證<br>
https://www.brilliantcode.net/343/centos-7-create-own-ssl-certificates/<br>
錯誤勘正 : step:4<br>
openssl x509 -req -days 3650 -in ca.csr -signkey ca.key -out ca.crt<br>
ca.key 前要空格<br>
<br>
<br>
</h1>DOCKER</h1><br>
<br>
docker pull 套件名:[版本]<br>
docker 網頁伺服器的家目錄 /usr/local/apache2/htdocs<br>
刪除docker 可參考<br>
https://www.cnblogs.com/zhenyuyaodidiao/p/4953143.html<br>
<br>
<br>
docker ps -a   可顯示已知的docker ps<br>
docker exec -it 目前容器ID ls  /路徑(給容器放的位置) <br>
docker commit ID user/套件:v2  凍結套件<br>
 <br>
<br>
https://hub.docker.com/<br>
<br>
docker pull httpd:2.4.41<br>
<br>
cd /tmp<br>
<br>
docker run -dit --name my-apache-app -p 8080:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4.41<br>
<br>
echo "hi" > hi.htm<br>
<br>
http://127.0.0.1:8080/hi.htm<br>

