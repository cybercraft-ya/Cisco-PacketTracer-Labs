
#### Routing Information Protocol (RIP) Network Design Based on Class-A: 

1.Basic Routing Configuration
2.IP Address Assign (DHCP configure)
3.RIP configuration
4.Routing Table Check
5.Response Checking


Step-1: Basic Router Configuration:
----------------------------------------
Router-0:
Router>enable
Router#configure terminal
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#int gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 12.0.0.1 255.0.0.0
Router(config-if)#exit

Router-1:
Router>enable
Router#configure terminal
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.0.2 255.0.0.0
Router(config-if)#exit
Router(config)#int gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 13.0.0.1 255.0.0.0
Router(config-if)#exit
Router(config)#int se0/0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 11.0.0.1 255.0.0.0
Router(config-if)#exit

Router-2:
Router>enable
Router#configure terminal
Router(config)#int se0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 11.0.0.2 255.0.0.0
Router(config-if)#exit
Router(config)#int gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 14.0.0.1 255.0.0.0
Router(config-if)#exit

Step-2: IP Address Assign (DHCP configure)
-----------------------------------------------------
Router-0:
Router(config)#ip dhcp pool branch0
Router(dhcp-config)#network 12.0.0.0 255.0.0.0
Router(dhcp-config)#default-router 12.0.0.1
Router(dhcp-config)#dns-server 8.8.8.8

Router-1:
Router(config)#ip dhcp pool branch1
Router(dhcp-config)#network 13.0.0.0 255.0.0.0
Router(dhcp-config)#default-router 12.0.0.1
Router(dhcp-config)#dns-server 8.8.8.8

Router-2:
Router(config)#ip dhcp pool branch2
Router(dhcp-config)#network 14.0.0.0 255.0.0.0
Router(dhcp-config)#default-router 12.0.0.1
Router(dhcp-config)#dns-server 8.8.8.8

Step-3: RIP-Routing Information Protocol Configuration
----------------------------------------------------------
Router-0:
Router(dhcp-config)#router rip
Router(config-router)#version 2
Router(config-router)#network 10.0.0.0
Router(config-router)#network 12.0.0.0

Router-1:
Router(dhcp-config)#router rip
Router(config-router)#version 2
Router(config-router)#network 10.0.0.0
Router(config-router)#network 11.0.0.0
Router(config-router)#network 13.0.0.0

Router-2:
Router(dhcp-config)#router rip
Router(config-router)#version 2
Router(config-router)#network 11.0.0.0
Router(config-router)#network 14.0.0.0

Step-4: Routing table check:
---------------------------------------------------------
Router#show ip route
Router#show running-config
Router#copy running-config startup-config

Step-5: Response Checking using ping command:
-------------------------------------------------------------
Terminal: ping 14.0.0.2
