#### EtherChannel Configuration
#### CDP-Cisco Discovery Protocol Configuration
#### NTP-Network Time Protocol Configuration

1.Ether Channel is configured on switches
2.Ether Channel can be configured both layer2 and layer3 switches.
3.Increases Speed
4.Create Redundency

#### EtherChannel Configuration
---------------------------------------------------- 
Switch-0:
Switch>enable
Switch#configure terminal	
Switch(config)#interface range fa0/1-2
Switch(config-if-range)#channel-group 2 mode  auto 
Switch(config-if-range)#switchport mode trunk

Switch-1:
Switch(config)#interface range fa0/1-2
Switch(config-if-range)#channel-group 2 mode  desirable
Switch(config-if-range)#switchport mode trunk
Switch# show etherchannel summary

#### CDP-Cisco Discovery Protocol Configuration
--------------------------------------------------------
1.CDP is used to get all information about routers and switches neighborship, model etc.

Router>enable
Router#configure terminal
Router(config)#interface gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)#exit

Router(config)#interface gig0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.20.1 255.255.255.0
Router(config-if)#exit
Router#show cdp neighbors


#### NTP-Network Time Protocol Configuration
1.IP Address of NTP server must be known by the router or core router.

Router-0:
Router>enable
Router#configure terminal
Router(config)#interface gig0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)#exit

Router(config)#ntp server 192.168.10.2 

N.B: Need 5 min to reset actual time and date
Router#show clock
11:24:19.597 UTC Tue Jul 22 2025