<h1>ansible</h1><br>
<br>
yum -y install ansible 在管理端下載就好<br>
erro　處理 <br>
(cryptography 0.8.2 (/usr/lib64/python2.7/site-packages),Requirement.parse('cryptography>=1.1')<br>
原因：cryptography 版本過低 需升級至1.1以上<br>
解決辦法: cryptography需要透過pip下載所以我們先下載pip
1.	安裝pip<br>
https://pypi.org/project/pip/#files<br>
下載pip-20.0.2.tar.gz <br>
tar zxvf pip-20.0.2.tar.gz<br>
cd pip-20.0.2<br>
python setup.py install<br>
2.[安裝wheel](https://pypi.org/project/wheel/#files)<br>

<br>
下載wheel-0.34.2.tar.gz<br>
tar -zxvf wheel-0.34.2.tar.gz<br>
cd wheel-0.34.2 python setup.py install<br>
<br>
3.[安裝cryptography 2.2.2](https://pypi.org/project/cryptography/)<br>
<br>
<br>

下載cryptography-2.2.2-cp27-cp27mu-manylinux1_x86_64.whl<br>
<br>
pip install cryptography-2.2.2-cp27-cp27mu-manylinux1_x86_64.whl<br>
<br>
參考資料<br>
[ansible自动化运维 cryptography 0.8.2 版本兼容性报错解决办法](https://blog.csdn.net/codemacket/article/details/80911149)<br>
<br>



