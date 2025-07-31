##### Switch Port Security Configuration
There two kinds of switch.
A.Layer-2 Switch
B.Layer-3 Switch

Switch port security is configured for preventing unauthorized access. Switch port can be secured in 3 ways, 
1.Protect (Does not generate log message/data)
2.Restrict (Generate Logs data) 
3.Shutdown (Generate logs data also shutdown the port)

Switch-0:
Switch>enable
Switch#configure terminal
Switch(config)#interface fa0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security maximum 1
Switch(config-if)#switchport port-security mac-address sticky 
Switch(config-if)#switchport port-security violation protect 

Switch(config-if)#interface fa0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security maximum 1
Switch(config-if)#switchport port-security mac-address sticky 
Switch(config-if)#switchport port-security violation restrict 
Switch(config-if)#exit

Switch(config)#interface fa0/4
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security maximum 1
Switch(config-if)#switchport port-security mac-address sticky
Switch(config-if)#switchport port-security violation shutdown

LAN_PC:
C:\> ping 192.168.10.1

Hacker_PC:
C:\> ping 192.168.10.1