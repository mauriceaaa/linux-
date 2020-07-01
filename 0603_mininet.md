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
~~~