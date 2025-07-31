#### NAT LAB TEST:
http://www.9tut.com/ccna-lab-sim/52-ccna-nat-sim-question

Question:
A network associate is configuring a router for the weaver company to provide internet access. The ISP has provided the company 
six public IP addresses of 198.18.184.105 198.18.184.110. The company has 14 hosts that need to access the internet simultaneously. 
The hosts in the company LAN have been assigned private space addresses in the range of 192.168.100.17 – 192.168.100.30.

The following have already been configured on the router：
- The basic router configuration
- The appropriate interfaces have been configured for NAT inside and NAT outside
- The appropriate static routes have also been configured (since the company will be a stub network, no routing protocol will be required.)
- All passwords have been temporarily set to "cisco"


NAT Configure:
------------------------------------------------------
Router>enable
Router#configure terminal
#### First you should change the router’s name to TUT
Router(config)#hostname TUT

#### Create a NAT pool of global addresses to be allocated with their netmask (/29 = 255.255.255.248). There were reports that the simulator in the real exam did not accept “prefix-length” keryword so you should use “netmask” keyword.
TUT(config)#ip nat pool mypool 198.18.184.105 198.18.184.110 netmask 255.255.255.248

#### Create a standard access control list that permits the addresses that are to be translated
TUT(config)#access-list 1 permit 192.168.100.16 0.0.0.15

#### Establish dynamic source translation, specifying the access list that was defined in the prior step
TUT(config)#ip nat inside source list 1 pool mypool overload

#### This command translates all source addresses that pass access list 1, which means a source address from 192.168.100.17 to 192.168.100.30, into an address from the pool named mypool (the pool contains addresses from 198.18.184.105 to 198.18.184.110)

#### Overload keyword allows to map multiple IP addresses to a single registered IP address (many-to-one) by using different ports

#### The question said that appropriate interfaces have been configured for NAT inside and NAT outside statements.

#### This is how to configure the NAT inside and NAT outside, just for your understanding:
TUT(config)#interface fa0/0
TUT(config-if)#ip nat inside
TUT(config-if)#exit
TUT(config)#interface s0/0
TUT(config-if)#ip nat outside
TUT(config-if)#end

tut#show ip nat translations

#### Finally, we should save all your work with the following command:
TUT#copy running-config startup-config

#### Check your configuration by going to “Host for testing” and type:
C:\>ping 192.0.2.114

