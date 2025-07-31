##### OSPF Multi-Area Network Design Based on Class-A:

1.Basic Router Configuration
2.IP Address Asign (DHCP configure)
3.OSPF Multi-Area Routing Protocol Configure
4.Routing Table Check/OSPF Check
7.Router Password Configure
8.Telnet or Remote Access

Step-1: Basic Router Configuration
------------------------------------------
Router-0:
Router>enable
Router#configure terminal
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#int gig0/0 
Router(config-if)#no shutdown
Router(config-if)#ip address 15.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#int se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 14.0.0.1 255.0.0.0
Router(config-if)#exit

Router-1:
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 11.0.0.2 255.0.0.0
Router(config-if)#exit
Router(config)#int gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 12.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#int se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 13.0.0.1 255.0.0.0
Router(config-if)#exit

Router-2:
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.0.2 255.0.0.0
Router(config-if)#exit
Router(config)#int se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 11.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#

Router-3:
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 13.0.0.2 255.0.0.0
Router(config-if)#exit
Router(config)#int se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 14.0.0.2 255.0.0.0
Router(config-if)#exit

Step-2: IP Address Assign (DHCP Configuration)
-------------------------------------------------------
Router-0:
Router(config)#ip dhcp pool branch0
Router(dhcp-config)#network 15.0.0.0 255.0.0.0
Router(dhcp-config)#default-router 15.0.0.1
Router(dhcp-config)#dns-server 8.8.8.8

Router-1:
Router(config)#ip dhcp pool branch1
Router(dhcp-config)#network 12.0.0.0 255.0.0.0
Router(dhcp-config)#default-router 12.0.0.1
Router(dhcp-config)#dns-server 8.8.8.8

Step-3: OSPF Multi-Area Routing Protocol Configuration
----------------------------------------------------------
Router-0:
Router(config)#router ospf 1
Router(config-router)#router-id 1.1.1.1
Router(config-router)#network 10.0.0.0 0.255.255.255 area 0
Router(config-router)#network 15.0.0.0 0.255.255.255 area 0
Router(config-router)#network 14.0.0.0 0.255.255.255 area 3

Router-1:
Router(config)#router ospf 1
Router(config-router)#router-id 2.2.2.2
Router(config-router)#network 11.0.0.0 0.255.255.255 area 1
Router(config-router)#network 12.0.0.0 0.255.255.255 area 1
Router(config-router)#network 13.0.0.0 0.255.255.255 area 2

Router-2:
Router(config)#router ospf 1
Router(config-router)#router-id 3.3.3.3
Router(config-router)#network 10.0.0.0 0.255.255.255 area 0
Router(config-router)#network 11.0.0.0 0.255.255.255 area 1

Router-3:
Router(config)#router ospf 1
Router(config-router)#router-id 4.4.4.4
Router(config-router)#network 13.0.0.0 0.255.255.255 area 2
Router(config-router)#network 14.0.0.0 0.255.255.255 area 3


Step-4: Router Password Configuration
--------------------------------------------------------
Console Password:
Line console 0
Password 1234
Login
Exit

Vty Password:
Line vty 0
Password 1234
Login
Eixt

Enable Password:
Enable secret 1234

All Password Encryption:
Service password-encryption