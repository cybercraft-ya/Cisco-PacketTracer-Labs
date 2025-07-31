##### ACL- Access Control List Configuration

1.Router Basic Configure
2.IP Address Assign
3.Gateway Check
4.ACL Configure
5.ACL Check

Pre-defined Limitations:
-------------------------------------
1.Host-A has permission to access Web-Server.
2.Host-A doesn’t have permission to access DHCP and DNS-Server.
3.Other Hosts have permission to access all servers.


Step-1: Router Basic Configure
--------------------------------------
Router>enable
Router#configure terminal
Router(config)#interface gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#exit

Router(config)#interface gig0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 20.0.0.1 255.0.0.0
Router(config-if)#exit

Step-2: IP Address Assign
------------------------------
….
Step-3: Gateway Check
------------------------------
….
Step-4: ACL Configure
------------------------------
Router>enable
Router#configure terminal
Router(config)#access-list 100 permit ip host 10.0.0.2 host 20.0.0.2
Router(config)#acces-list 100 deny ip host 10.0.0.2 20.0.0.0 0.255.255.255	
Router(config)#access-list 100 deny ip host 10.0.0.2 20.0.0.0 0.255.255.255
Router(config)#access-list 100 permit ip any any
Router(config)#int gig0/1
Router(config-if)#ip access-group 100 out

Step-5: ACL Check
---------------------------
Host-A Terminal: 
C:\> Ping 20.0.0.2
C:\> Ping 20.0.0.3
C:\> Ping 20.0.0.4