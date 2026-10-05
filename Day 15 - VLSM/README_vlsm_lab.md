# VLSM Subnetting Lab

This lab was all about hands-on practice with subnetting, specifically VLSM (Variable Length Subnet Mask).

Network used: **192.168.5.0/24**

## Task 1: Calculate Each LAN's Needs

I started with the largest LAN and worked down.

### LAN2: 64 hosts

- A /25 prefix length is needed, because /25 provides 126 usable addresses (/26 would provide only 62, which is not enough).
- **Network address:** 192.168.5.0
- **Broadcast address:** 192.168.5.127 (all host bits set to 1: `192.168.5.0|1111111`)

### LAN1: 45 hosts

- A /26 prefix length will suffice (62 usable addresses).
- **Network address:** 192.168.5.128
- **Broadcast address:** 192.168.5.191

### LAN3: 14 hosts

- A /28 prefix length will be used (14 usable addresses).
- **Network address:** 192.168.5.192
- **Broadcast address:** 192.168.5.207

### LAN4: 9 hosts

- A /28 will be used once again, because a /29 would be too small (it provides only 6 usable addresses).
- **Network address:** 192.168.5.208
- **Broadcast address:** 192.168.5.223

### Point-to-point link between R1 and R2

- A /30 is used, which provides two usable addresses. On a point-to-point link a /31 could be used as well, because a network and broadcast address are not necessary in that case.
- **Network address:** 192.168.5.224
- **Broadcast address:** 192.168.5.227

### Summary

| Segment | Hosts needed | Prefix | Network | Broadcast |
|---|---|---|---|---|
| LAN2 | 64 | /25 | 192.168.5.0 | 192.168.5.127 |
| LAN1 | 45 | /26 | 192.168.5.128 | 192.168.5.191 |
| LAN3 | 14 | /28 | 192.168.5.192 | 192.168.5.207 |
| LAN4 | 9 | /28 | 192.168.5.208 | 192.168.5.223 |
| R1-R2 link | 2 | /30 | 192.168.5.224 | 192.168.5.227 |

## Task 2: Configuration

After these calculations I completed the tasks, which were:

1. Assign the first usable address to the PC in each LAN.
2. Assign the last usable address to the router's interface in each LAN.
3. Configure static routes so that all PCs can ping each other.

### R1

```
R1(config-if)#do sh ip int br
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.5.190   YES manual up                    up
GigabitEthernet0/1     192.168.5.126   YES manual up                    up
GigabitEthernet0/0/0   192.168.5.225   YES manual up                    up
```

Static routes:

```
S       192.168.5.192/28 [1/0] via 192.168.5.226
S       192.168.5.208/28 [1/0] via 192.168.5.226
```

### R2

```
R2(config-if)#do sh ip int br
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.5.206   YES manual up                    up
GigabitEthernet0/1     192.168.5.222   YES manual up                    up
GigabitEthernet0/0/0   192.168.5.226   YES manual up                    up
```

Static routes:

```
S       192.168.5.0/25 [1/0] via 192.168.5.225
S       192.168.5.128/26 [1/0] via 192.168.5.225
```

> Lab file from Jeremy's IT Lab's Free CCNA Course.
