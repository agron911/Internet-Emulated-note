# cisco ptracer

* 下載cisco ptracer:

1.連mikrotik教室網路
```
http://192.168.60.133/smallko/ptracer.zip
```
2.連無線網路
```
http:/csie.ngu.edo.tw/smallko/ptracer.zip
```

##
1.POST(post on self test) //開機自檢系統
2.start-up configuration
3.running configuration 




## 路由器 使用找資料控制

頻內 / 頻外 (In-Band / Out-of-Band)
https://www.digitimes.com.tw/tw/dt/n/shwnws.asp?cnlid=10&cat=&cat1=&id=109018

* in band
** 透過talnet ssh
* out of band
** 透過console

## 指令
```
> enable  //特權模式
> ?       //顯示功能
> exit    //回上一頁
> configure terminal
> do show running //可看 running-config
# show ip int brief //顯示所有介面卡
```

## 兩台主機互聯
先拉一台Router-PT , PC0 , PC1
* 用console線將router,pc0 連起來。 
* 用copper cross-over 連pc0, pc1，右鍵選擇ether

pc0
```
# configure terminal
# int f0/0
# ip address 192.168.1.1 255.255.255.0
# no shutdown
```
pc1 進入到config 設定fastethernet
```
將ip configuration改成static
設置IP address 和subnet Mask
```

## write 
PC0
```
> enable
# configure terminal
# enable password cisco
# show ip int brief
# int f0/0
# ip address 192.168.1.1 255.255.255.0
# no shutdown 
# copy running-configuration start-up configuration
# reload
>enable
# erase start-up configuration
# write
#copy running-configuration start-up configuration
# show running-config
# hostname agron
# show int f0/0

```

## 讓機器可以實現telnet , in band 
* 一台機器只有一個console port

PC0
```
# conf t
# line vty 0 4
# password 1234
# enable password cisco
```
PC1
```
> telnet 192.168.1.1
```

## 增加使用者
PC0
```
> enable
# conf t
# username tom password tom
# line vty 0 4 
# no password
# login local
```
PC1
```
>telnet 192.168.1.1 //user: tom   password:tom
```

## 破解 cisco 路由器密碼
* 必須先做``` # write ```
路由器忘記密碼
先關機，開機時按下 ctrl+break
```
> confreg 0x2142
> boot
```
成功重啟， 開始找回以前資料
```
> enable
# copy startup-configuration running-configuration
# conf t
# config-register 0x2102
# enable password 1234
# enable secret 1234
```

