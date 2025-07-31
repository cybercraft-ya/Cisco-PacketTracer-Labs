
##### VPN - Virtual Private Network Configuration

1.Router Basic Configuration
2.DHCP Configure
3.Gateway Check
4.Routing Protocol Configure
5.Routing Protocol Check
6.VPN Configure
7.VPN Check

1.Router Basic Configuration
---------------------------------------------------
Router-0:
Router>enable
Router#configure terminal
Router(config)#interface se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.10.2 255.255.255.0
Router(config-if)#exit
Router(config)#interface se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.11.1 255.255.255.0
Router(config-if)#exit
Router(config)#


Router-1: 
Router>enable
Router#configure terminal
Router(config)#interface se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)#exit
Router(config)#interface gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.12.1 255.255.255.0
Router(config-if)#exit

Router-2:
Router>enable
Router#configure terminal
Router(config)#interface se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.11.2 255.255.255.0
Router(config-if)#exit
Router(config)#interface gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.13.1 255.255.255.0
Router(config-if)#exit
Router(config)#


2.IP Address Assign..
-------------------------------------------------------
Router-1:
Router(config)#ip dhcp pool office1
Router(dhcp-config)#network 192.168.12.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.12.1
Router(dhcp-config)#dns-server 8.8.8.8
Router(dhcp-config)#exit

Router-2:
Router(config)#ip dhcp pool office2
Router(dhcp-config)#network 19.168.13.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.13.1
Router(dhcp-config)#dns-server 8.8.8.8
Router(dhcp-config)#exit


3.Gateway Check
--------------------------------------------------------
.....

4.Routing Protocol Configure
------------------------------------------------------
Router-0:
Router(config)#router eigrp 10
Router(config-router)#eigrp router-id 2.2.2.2
Router(config-router)#network 192.168.10.0 255.255.255.0
Router(config-router)#network 192.168.11.0 255.255.255.0
Router(config-router)#exit

Router-1:
Router(config)#router eigrp 10
Router(config-router)#eigrp router-id 1.1.1.1
Router(config-router)#network 192.168.10.0 255.255.255.0
Router(config-router)#network 192.168.12.0 255.255.255.0
Router(config-router)#exit

Router-2:
Router(config)#router eigrp 10
Router(config-router)#eigrp router-id 3.3.3.3
Router(config-router)#network 192.168.11.0 255.255.255.0
Router(config-router)#
Router(config-router)#network 192.168.13.0 255.255.255.0
Router(config-router)#exit

6.VPN Configure
----------------------------------------------------------
Router-1: 
Router(config)#interface tunnel 0
Router(config-if)#ip address 100.0.0.1 255.0.0.0
Router(config-if)#tunnel source se0/0/0
Router(config-if)#tunnel destination 192.168.11.2

Router-2:
Router(config)#interface tunnel 0
Router(config-if)#ip address 100.0.0.1 255.0.0.0
Router(config-if)#tunnel source se0/0/0
Router(config-if)#tunnel destination 192.168.10.1