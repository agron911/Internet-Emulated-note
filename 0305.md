# INTERNET EMULATER AND ANALYSIS

## 進入mininet
```
*links
*net
*link h1 r1 up //可以利用了解網路連結狀態
```
## 開啟主機
```
xterm h1 
xterm h2 
xterm h3 
xterm r1 
```
## 清除主機上的介面卡，並增加新的介面卡
h1
```
ifconfig h1-eth0 0
ip addr add 192.168.1.1/24 brd + dev h1-eth0
ip route add default via 192.168.1.254
```
h2
```
ifconfig h2-eth0 0
ip addr add 192.168.2.1/24 brd + dev h2-eth0
ip route add default via 192.168.2.254
```
h3
```
ifconfig h3-eth0 0
ip addr add 192.168.3.1/24 brd + dev h2-eth0
ip route add default via 192.168.3.254
```
## 路由器
r1
```
ifconfig r1-eth0 0
ip addr add 192.168.1.254/24 brd + dev r1-eth0
ip addr add 192.168.2.254/24 brd + dev r1-eth1
ip addr add 192.168.3.254/24 brd + dev r1-eth2
```
ip route add default via 192.168.1.254
ip route del


