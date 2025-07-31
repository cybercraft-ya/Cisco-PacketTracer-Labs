
#### Static Routing Protocol Design Based on Class-C
Step 1: Basic Router Configuration 
Step 2: IP address Assign/DHCP Configure 
Step 3: Gateway Check
Step 4: Static Routing Configuration 
Step 5: Routing Table Check 


Step1: Router Basic Configuration.
#----------------------------------------
Router-0:
Router> Enable
Router# Configure terminal
Router (config)# Int se0/0/0
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.10.1 255.255.255.0
Router (config-if)# Exit
Router (config)# Int gig0/0
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.12.1 255.255.255.0
Router (config-if)# Exit

Router-1:
Router (config-if)# Int se0/1/0
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.10.2 255.255.255.0
Router (config-if)# Exit
Router (config-if)# Int gig0/0
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.13.1 255.255.255.0
Router (config-if)# Exit
Router (config-if)# Int se0/0/1
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.11.1 255.255.255.0
Router (config-if)# Exit

Router-2:
Router (config-if)# Int se0/1/1
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.11.2 255.255.255.0
Router (config-if)# Exit
Router (config-if)# Int gig0/0
Router (config-if)# No shutdown
Router (config-if)# Ip address 192.168.14.1 255.255.255.0
Router (config-if)# exit

Step2: IP Address Assign (DHCP- Dynamic Host Configuration Protocol)
#----------------------------------------
Router-0:
Router (config-if)# IP dhcp pool room01
Router (config-if)# Network 192.168.12.0 255.255.255.0
Router (config-if)# Default-router 192.168.12.1
Router (config-if)# Dns-server 8.8.8.8

Router-1:
Router (config-if)# Ip dhcp pool room02
Router (config-if)# Network 192.168.13.0 255.255.255.0
Router (config-if)# Default-router 192.168.13.1
Router (config-if)# Dns-server 8.8.8.8

Router-2:
Router (config-if)# Ip dhcp pool room03
Router (config-if)# Network 192.168.14.0 255.255.255.0
Router (config-if)# Default-router 192.168.14.1
Router (config-if)# Dns-server 8.8.8.8

Step3: Router Gateway check
#----------------------------------------
c:\> ping 192.168.10.1


Step4: Static Routing Configuration.
#----------------------------------------
Router-0:
Router (config-if)# Ip route 192.168.11.0 255.255.255.0 192.168.10.2
Router (config-if)# Ip route 192.168.13.0 255.255.255.0 192.168.10.2
Router (config-if)# Ip route 192.168.14.0 255.255.255.0 192.168.10.2

Router-1:
Router (config-if)# Ip route 192.168.12.0 255.255.255 192.168.10.1
Router (config-if)# Ip route 192.168.14.0 255.255.255.0 192.168.11.2

Router-2:
Router (config-if)# Ip route 192.168.10.0 255.255.255.0 192.168.11.1
Router (config-if)# Ip route 192.168.12.0 255.255.255.0 192.168.11.1
Router (config-if)# Ip route 192.168.13.0 255.255.255.0 192.168.11.1

Step5: Routing Table Check.
#----------------------------------------
Rotuer# Show ip route
Router# Show running-config
Router# Copy running-config startup-config (to save startup configuration)