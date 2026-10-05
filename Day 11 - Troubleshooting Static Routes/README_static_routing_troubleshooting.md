# Static Routing Troubleshooting Lab

I found and fixed three misconfigurations in this lab.

## Misconfiguration 1: Wrong next hop on R1

In Router 1's routing table there is a static route to 192.168.3.0/24 via 192.168.12.3. The address 192.168.12.3 isn't configured anywhere; 192.168.12.2 is. The next hop should be 192.168.12.2.

**Router 1 routing table (before):**

```
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, GigabitEthernet0/1
L       192.168.1.254/32 is directly connected, GigabitEthernet0/1
S    192.168.3.0/24 [1/0] via 192.168.12.3
     192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.12.0/24 is directly connected, GigabitEthernet0/0
L       192.168.12.1/32 is directly connected, GigabitEthernet0/0
```

**Router 1 routing table (after fix):**

```
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, GigabitEthernet0/1
L       192.168.1.254/32 is directly connected, GigabitEthernet0/1
S    192.168.3.0/24 [1/0] via 192.168.12.2
     192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.12.0/24 is directly connected, GigabitEthernet0/0
L       192.168.12.1/32 is directly connected, GigabitEthernet0/0
```

## Misconfiguration 2: Wrong exit interface on R2

In Router 2's routing table the static route to 192.168.3.0/24 has G0/0 as its exit interface, which is wrong. It should be G0/1.

**Router 2 routing table (before):**

```
S    192.168.1.0/24 [1/0] via 192.168.12.1
S    192.168.3.0/24 is directly connected, GigabitEthernet0/0
     192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.12.0/24 is directly connected, GigabitEthernet0/0
L       192.168.12.2/32 is directly connected, GigabitEthernet0/0
     192.168.13.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.13.0/24 is directly connected, GigabitEthernet0/1
L       192.168.13.2/32 is directly connected, GigabitEthernet0/1
```

**Router 2 routing table (after fix):**

```
S    192.168.1.0/24 [1/0] via 192.168.12.1
S    192.168.3.0/24 is directly connected, GigabitEthernet0/1
     192.168.12.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.12.0/24 is directly connected, GigabitEthernet0/0
L       192.168.12.2/32 is directly connected, GigabitEthernet0/0
     192.168.13.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.13.0/24 is directly connected, GigabitEthernet0/1
L       192.168.13.2/32 is directly connected, GigabitEthernet0/1
```

## Misconfiguration 3: Wrong IP address on R3

In Router 3's interface configuration, G0/0 was configured with 192.168.23.3 instead of 192.168.13.3 as the diagram shows.

**Interface configuration (before):**

```
R3#sh ip int br
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.23.3    YES manual up                    up
GigabitEthernet0/1     192.168.3.254   YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

**Interface configuration (after fix):**

```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.13.3    YES manual up                    up
GigabitEthernet0/1     192.168.3.254   YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down
```

## Verification: PC1 pinging PC2

```
C:\>ping 192.168.3.1

Pinging 192.168.3.1 with 32 bytes of data:

Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
Reply from 192.168.3.1: bytes=32 time<1ms TTL=125
```

> Lab file from Jeremy's IT Lab's Free CCNA Course.
