# netw_hw4

![image](https://user-images.githubusercontent.com/68617720/206926362-051c1a15-a13e-4cb9-8539-96d24395b329.png)
___
Для R1:
```Router>enable
Router#conf t
Router(config)#interface e0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.10.1 255.255.255.0
Router(config-if)#exit
Router(config)#interface e0/1
Router(config-if)#ip address 1.1.10.2 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)#interface Tunnel100
Router(config-if)#ip address 172.16.10.1 255.255.255.0
Router(config-if)#ip mtu 1400
Router(config-if)#ip tcp adjust-mss 1360
Router(config-if)# tunnel source 1.1.10.2
Router(config-if)#tunnel destination 1.1.20.2
Router(config-if)#exit
Router(config)#ip route 0.0.0.0 0.0.0.0 1.1.10.1
Router(config)#ip route 10.0.20.2 255.255.255.255 172.16.10.2

Router(config)#interface Tunnel200
Router(config-if)#ip address 172.16.11.1 255.255.255.0
Router(config-if)#ip mtu 1400
Router(config-if)#ip tcp adjust-mss 1360
Router(config-if)#tunnel source 1.1.10.2
Router(config-if)#tunnel destination 1.1.30.2
Router(config-if)#exit

Router(config)#crypto isakmp policy 1
Router(config-isakmp)#encr 3des
Router(config-isakmp)#hash md5
Router(config-isakmp)#authentication pre-share
Router(config-isakmp)#group 2
Router(config-isakmp)#lifetime 86400
Router(config-isakmp)#exit
Router(config)#crypto isakmp key merionet address 1.1.30.2
Router(config)#crypto ipsec transform-set TS esp-3des esp-md5-hmac
Router(cfg-crypto-trans)#mode transport
Router(cfg-crypto-trans)#exit
Router(config)#crypto ipsec profile protect-gre
Router(ipsec-profile)#set security-association lifetime seconds 86400
Router(ipsec-profile)#set transform-set TS
Router(ipsec-profile)#exit
Router(config)#interface Tunnel200
Router(config-if)# tunnel protection ipsec profile protect-gre
Router(config-if)#exit
```
___
Для R2: 
```Router>enable
Router#conf t
Router(config)#interface e0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 1.1.10.1 255.255.255.0
Router(config-if)#exit
Router(config)#interface e0/1
Router(config-if)#ip address 1.1.20.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#exit
```
___
Для R3:
```Router>enable
Router#conf t
Router(config)#interface e0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 1.1.20.2 255.255.255.0
Router(config-if)#interface e0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.20.1 255.255.255.0
Router(config)#exit
Router(config)#interface Tunnel100
Router(config-if)#ip address 172.16.10.2 255.255.255.0
Router(config-if)# ip mtu 1400
Router(config-if)# ip tcp adjust-mss 1360
Router(config-if)# tunnel source 1.1.20.2
Router(config-if)#tunnel destination 1.1.10.2
Router(config-if)#exit
Router(config)#ip route 0.0.0.0 0.0.0.0 1.1.20.1
Router(config)#ip route 10.0.10.2 255.255.255.255 172.16.10.1
Router(config)#exit
```
___
Для R4:
```Router>enable
Router#conf t
Router(config)#interface e0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 1.1.30.2 255.255.255.0
Router(config-if)#exit
Router(config)#interface e0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.30.1 255.255.255.0
Router(config-if)#exit
Router(config)#interface Tunnel200
Router(config-if)#ip address 172.16.11.2 255.255.255.0
Router(config-if)#ip mtu 1400
Router(config-if)#ip tcp adjust-mss 1360
Router(config-if)#tunnel source 1.1.30.2
Router(config-if)#tunnel destination 1.1.10.2
Router(config-if)#exit
Router(config)#ip route 0.0.0.0 0.0.0.0 1.1.30.1
Router(config)#exit
Router(config)#ip route 10.0.10.2 255.255.255.255 172.16.11.1

Router(config)#crypto isakmp policy 1
Router(config-isakmp)#encr 3des
Router(config-isakmp)#hash md5
Router(config-isakmp)#authentication pre-share
Router(config-isakmp)#group 2
Router(config-isakmp)#lifetime 86400
Router(config-isakmp)#exit
Router(config)#crypto isakmp key merionet address 1.1.10.2
Router(config)#crypto ipsec transform-set TS esp-3des esp-md5-hmac
Router(cfg-crypto-trans)#mode transport
Router(cfg-crypto-trans)#exit
Router(config)#crypto ipsec profile protect-gre
Router(ipsec-profile)#set security-association lifetime seconds 86400
Router(ipsec-profile)#set transform-set TS
Router(ipsec-profile)#exit
Router(config)#interface Tunnel 200
Router(config-if)#tunnel protection ipsec profile protect-gre
Router(config-if)#exit
Router(config)#exit
```
___
Для VPC5:
```ip 10.0.10.2 255.255.255.0 10.0.10.1```
___
Для VPC6:
```ip 10.0.20.2 255.255.255.0 10.0.20.1```
___
Для VPC7:
```ip 10.0.20.2 255.255.255.0 10.0.20.1```
