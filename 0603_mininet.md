- 準備一個 ubuntu 環境<br>
- 使用 python 創建 mininet<br>
<br>
腳本內容:<br>
~~~
#!/usr/bin/python

from mininet.net import Mininet
from mininet.node import Host
from mininet.cli import CLI
from mininet.link import TCLink, Intf
from mininet.log import setLogLevel, info
from subprocess import call

def myNetwork():
    net = Mininet(topo=None, build=False)

    r1 = net.addHost('r1')
    h3 = net.addHost('h3')
    h2 = net.addHost('h2')
    h1 = net.addHost('h1')

    info( '*** Add links\n')
    mylink = {'bw':10,'delay':'1ms','loss':0}  
             # bw 頻寬、delay 延遲、loss 遺失
    net.addLink(h1, r1, cls=TCLink , **mylink)
    net.addLink(h2, r1, cls=TCLink , **mylink)
    net.addLink(h3, r1, cls=TCLink , **mylink)

    info( '*** Starting network\n')
    net.build()

    # 清除網路卡 ip
    h1.cmd("ifconfig h1-eth0 0")
    h2.cmd("ifconfig h2-eth0 0")
    h3.cmd("ifconfig h3-eth0 0")
    r1.cmd("ifconfig r1-eth0 0")
    r1.cmd("ifconfig r1-eth1 0")
    r1.cmd("ifconfig r1-eth2 0")
    
    # 啟動路由器
    r1.cmd("echo 1 > /proc/sys/net/ipv4/ip_forward")
    r1.cmd("ip addr add 192.168.1.254/24 brd + dev r1-eth0")
    r1.cmd("ip addr add 192.168.2.254/24 brd + dev r1-eth1")
    r1.cmd("ip addr add 192.168.3.254/24 brd + dev r1-eth2")  

    h1.cmd("ip addr add 192.168.1.1/24 brd + dev h1-eth0")
    h1.cmd("ip route add default via 192.168.1.254")
    h2.cmd("ip addr add 192.168.2.1/24 brd + dev h2-eth0")
    h2.cmd("ip route add default via 192.168.2.254")
    h3.cmd("ip addr add 192.168.3.1/24 brd + dev h3-eth0")
    h3.cmd("ip route add default via 192.168.3.254")

    
    CLI(net)
    net.stop()
    if __name__ == '__main__':
    setLogLevel( 'info' )
    myNetwork()


執行之後開啟終端機 <br> 
mininet> xterm h1 h2<br>
(會開啟兩個終端)<br>


<br>
<h1>lvs</h1>

~~~
 from mininet.net import Containernet    # mininet 的加強版，有支援 Docker
 from mininet.cli import CLI
 from mininet.link import Link,TCLink,Intf
 from mininet.log import setLogLevel
 from mininet.node import Docker
 from time import sleep

 if '__main__' == __name__:
    setLogLevel('info')
    net = Containernet(link=TCLink)
    h1 = net.addHost('h1',ip="10.0.1.1/24")
    r = net.addHost('r')    # 產生一台路由器

    # Docker
    h2 = net.addDocker('h2', mac = '00:00:00:00:02:02', ip="10.0.2.2/24", dimage="smallko/php-apache-dev:v10",cpu_period=50000, cpu_quota=1000)
    h3 = net.addDocker('h3', mac = '00:00:00:00:03:03', ip="10.0.3.3/24", dimage="smallko/php-apache-dev:v10",cpu_period=50000, cpu_quota=1000)
    h4 = net.addDocker('h4', mac = '00:00:00:00:04:04', ip="10.0.4.4/24", dimage="smallko/php-apache-dev:v10",cpu_period=50000, cpu_quota=1000)
    net.addLink(h1, r, cls=TCLink, bw=10)
    net.addLink(h2, r, cls=TCLink, bw=10)
    net.addLink(h3, r, cls=TCLink, bw=10)
    net.addLink(h4, r, cls=TCLink, bw=10)
    net.start()
    h1,h2,h3,h4,r=net.get('h1','h2','h3','h4','r')
    r.cmd("ifconfig r-eth0 0")
    r.cmd("ifconfig r-eth1 0")
    r.cmd("ifconfig r-eth2 0")
    r.cmd("ifconfig r-eth3 0")
    r.cmd("echo 1 > /proc/sys/net/ipv4/ip_forward")
    r.cmd("ip addr add 10.0.1.254/24 brd + dev r-eth0")
    r.cmd("ip addr add 10.0.2.254/24 brd + dev r-eth1")
    r.cmd("ip addr add 10.0.3.254/24 brd + dev r-eth2")
    r.cmd("ip addr add 10.0.4.254/24 brd + dev r-eth3")
    r.cmd("iptables -t nat -A POSTROUTING -s 10.0.2.0/24 -o r-eth0  -j MASQUERADE")
    r.cmd("iptables -t nat -A POSTROUTING -s 10.0.3.0/24 -o r-eth0  -j MASQUERADE")
    r.cmd("iptables -t nat -A POSTROUTING -s 10.0.4.0/24 -o r-eth0  -j MASQUERADE")
    r.cmd("ipvsadm -A -t 10.0.1.254:80 -s rr")
    r.cmd("ipvsadm -a -t 10.0.1.254:80 -r 10.0.2.2:80 -m")
    r.cmd("ipvsadm -a -t 10.0.1.254:80 -r 10.0.3.3:80 -m")
    r.cmd("ipvsadm -a -t 10.0.1.254:80 -r 10.0.4.4:80 -m")
    h1.cmd("ip route add default via 10.0.1.254")
    h2.cmd("ip route del default")
    h2.cmd("ip route add default via 10.0.2.254")
    h2.cmd("cd /var/www/html; echo h2 > a.htm ; python -m SimpleHTTPServer 80 &")
    h3.cmd("ip route del default")
    h3.cmd("ip route add default via 10.0.3.254")
    h3.cmd("cd /var/www/html; echo h3 > a.htm ; python -m SimpleHTTPServer 80 &")
    h4.cmd("ip route del default")
    h4.cmd("ip route add default via 10.0.4.254")
    h4.cmd("cd /var/www/html; echo h4 > a.htm ; python -m SimpleHTTPServer 80 &")
    CLI(net)
    net.stop()
    ~~~

