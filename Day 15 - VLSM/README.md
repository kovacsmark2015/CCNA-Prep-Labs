This lab was all about hands on practice with subnetting specifically VLSM (Variable Length Subnet Mask).

Working with the network 192.168.5.0/24

First task was to calculate each LAN's needs.

Starting with the largest LAN:



LAN2 - 64 hosts

For 64 hosts It needs a /25 prefix length because /25 provides 126 usable addresses (/26 would provide 62 which is not enough).

The Network address is the first address in the range which is: 192.168.5.0

The Broadcast address is the last address in the range which is: 192.168.5.127 (setting all the host bits to 1 -> 192.168.5.0|1111111)



LAN1 - 45 hosts



For 45 hosts a /26 prefix length will suffice. (providing 62 usable addresses).

The Network Address is: 192.168.5.128

The Broadcast Address is: 192.168.5.191



LAN3 - 14 hosts



For 14 hosts a /28 prefix length will be used. (providing 14 usable addresses)

The Network Address is: 192.168.5.192

The Broadcast Address is: 192.168.5.207



LAN4 - 9 hosts



For 9 hosts a /28 will be used once again because a /29 would be too small(it would provide 6 usable addresses)

The Network Address is: 192.168.5.208

The Broadcast Address is: 192.168.5.223



Point-to-Point link between R1 and R2



/30 (/31), /30 provides two usable addresses. In a point-to-point connection a /31 could be used as well because a network and a broadcast address is not necessary in this case.



The Network Address is: 192.168.5.224

The Broadcast Address is: 192.168.5.227



After these calculations I completed the tasks, which were:

I assigned the first usable address to the PC in each LAN.

I assigned the last usable address to the router's interface in each LAN

I configured static routes so that all PC-s were able to ping each other.



R1 Config:

*R1(config-if)#do sh ip int br*

*Interface              IP-Address      OK? Method Status                Protocol* 

*GigabitEthernet0/0     192.168.5.190   YES manual up                    up* 

*GigabitEthernet0/1     192.168.5.126   YES manual up                    up* 

*GigabitEthernet0/0/0   192.168.5.225   YES manual up                    up* 



*S       192.168.5.192/28 \[1/0] via 192.168.5.226*

*S       192.168.5.208/28 \[1/0] via 192.168.5.226*



R2 Config:

*R2(config-if)#do sh ip int br*

*Interface              IP-Address      OK? Method Status                Protocol* 

*GigabitEthernet0/0     192.168.5.206   YES manual up                    up* 

*GigabitEthernet0/1     192.168.5.222   YES manual up                    up* 

*GigabitEthernet0/0/0   192.168.5.226   YES manual up                    up* 



*S       192.168.5.0/25 \[1/0] via 192.168.5.225*

*S       192.168.5.128/26 \[1/0] via 192.168.5.225*



Lab file from Jeremy's It Lab's Free CCNA Course



