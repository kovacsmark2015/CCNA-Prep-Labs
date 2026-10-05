1.Misconfig:

In Router 1's routing table there is a static route to 192.168.3.0/24 via 192.168.12.3.

192.168.12.3 isn't configured, 192.168.12.2 is. It is the next hop IP.

Router 1 Routing table:

&#x20;    *192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.1.0/24 is directly connected, GigabitEthernet0/1*

*L       192.168.1.254/32 is directly connected, GigabitEthernet0/1*

*S    192.168.3.0/24 \[1/0] via 192.168.12.3*

&#x20;    *192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.12.0/24 is directly connected, GigabitEthernet0/0*

*L       192.168.12.1/32 is directly connected, GigabitEthernet0/0*

Router 1 Routing table after fix:

&#x20;    *192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.1.0/24 is directly connected, GigabitEthernet0/1*

*L       192.168.1.254/32 is directly connected, GigabitEthernet0/1*

*S    192.168.3.0/24 \[1/0] via 192.168.12.2*

&#x20;    *192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.12.0/24 is directly connected, GigabitEthernet0/0*

*L       192.168.12.1/32 is directly connected, GigabitEthernet0/0*



2.Misconfig:



In Router 2's routing table the static route to 192.168.3.0/24 has G0/0 as it's exit interface which is wrong (should be g0/1).

Router 2 Routing table:

*S    192.168.1.0/24 \[1/0] via 192.168.12.1*

*S    192.168.3.0/24 is directly connected, GigabitEthernet0/0*

&#x20;    *192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.12.0/24 is directly connected, GigabitEthernet0/0*

*L       192.168.12.2/32 is directly connected, GigabitEthernet0/0*

&#x20;    *192.168.13.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.13.0/24 is directly connected, GigabitEthernet0/1*

*L       192.168.13.2/32 is directly connected, GigabitEthernet0/1*



Router 2 Routing table after fix:

*S    192.168.1.0/24 \[1/0] via 192.168.12.1*

*S    192.168.3.0/24 is directly connected, GigabitEthernet0/1*

&#x20;    *192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.12.0/24 is directly connected, GigabitEthernet0/0*

*L       192.168.12.2/32 is directly connected, GigabitEthernet0/0*

&#x20;    *192.168.13.0/24 is variably subnetted, 2 subnets, 2 masks*

*C       192.168.13.0/24 is directly connected, GigabitEthernet0/1*

*L       192.168.13.2/32 is directly connected, GigabitEthernet0/1*



3.Misconfig:

In Router 3's interface config G0/0-s IP is configured as 192.168.23.3 instead of 192.168.13.3 as the diagram shows.

Interface configuration

*R3#sh ip int br*

*Interface              IP-Address      OK? Method Status                Protocol* 

*GigabitEthernet0/0     192.168.23.3    YES manual up                    up* 

*GigabitEthernet0/1     192.168.3.254   YES manual up                    up* 

*GigabitEthernet0/2     unassigned      YES unset  administratively down down* 

*Vlan1                  unassigned      YES unset  administratively down down*

Interface configuration after fix:

*Interface              IP-Address      OK? Method Status                Protocol* 

*GigabitEthernet0/0     192.168.13.3    YES manual up                    up* 

*GigabitEthernet0/1     192.168.3.254   YES manual up                    up* 

*GigabitEthernet0/2     unassigned      YES unset  administratively down down* 

*Vlan1                  unassigned      YES unset  administratively down down*

PC1 pinging PC2
C:\>ping 192.168.3.1

Pinging 192.168.3.1 with 32 bytes of data:

Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125


Lab file from Jeremy's It Lab's Free CCNA Course



