##### VLAN - Virtual Local Area Network Configuration

Switch-0:
Switch(config)#vlan 2
Switch(config-vlan)#name sales
Switch(config-vlan)#exit

Switch(config)#vlan 3
Switch(config-vlan)#name IT
Switch(config-vlan)#exit
Switch(config)#interface range fa0/2-3
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 2
Switch(config-if-range)#exit

Switch(config)#interface range fa0/4-5
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 3
Switch(config-if-range)#exit
                ^
Switch(config)#interface fa0/1
Switch(config-if)#switchport mode trunk
Switch#show vlan brief

Switch-1:
Switch#configure terminal
Switch(config)#vlan 2
Switch(config-vlan)#name sales
Switch(config-vlan)#exit

Switch(config)#vlan 3
Switch(config-vlan)#name IT
Switch(config-vlan)#exit

Switch(config)#interface range fa0/2-3
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 2
Switch(config-if-range)#exit

Switch(config)#interface range fa0/4-5
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 3
Switch(config-if-range)#exit

Switch(config)#interface fa0/1
Switch(config-if)#switchport mode trunk

Router-0:
Router(config)#interface gig0/0
Router(config)#no shutdown
Router(config)#exit

Router(config)#interface gig0/0.1
Router(config-subif)#no shutdown
Router(config-subif)#encapsulation dot1Q  2
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)#exit

Router(config)#interface gig0/0.2
Router(config-subif)#no shutdown
Router(config-subif)#encapsulation dot1Q  3
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)#exit

Switch(config)#interface fa0/6
Switch(config-if)#switchport mode trunk
Switch#show vlan brief



